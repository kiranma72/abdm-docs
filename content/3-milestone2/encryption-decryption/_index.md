+++
title = "Encryption & Decryption"
date = 2023-04-11T05:10:00+05:30
weight = 8
chapter = true
pre = "<b>3.8 </b>"
+++

# Encryption and Decryption

The following **abbreviations** are used in this section:

- ECDH: Elliptic-curve Diffie–Hellman Key Exchange
- AES-GCM: Advanced Encryption Standard-Galois/Counter Mode
- DHPK: Elliptic-curve Diffie–Hellman public key
- DHSK: Elliptic-curve Diffie–Hellman secret/private key
- P and U is annotation for system
- DHK(U,P): Elliptic-curve Diffie–Hellman Key
- Rand: Random String

Information shared as part of the data flow will be **secured using an encryption mechanism that ensures perfect forward secrecy.**

This means that even if any of the key materials stored at HIPs, HIUs or HDCM clients (either long-term private keys or session keys) are compromised, it would not be possible to decipher data that was previously exchanged. 

The encryption mechanism uses **Elliptic-curve Diffie–Hellman Key Exchange (ECDH),** which is used in many Internet protocols such as SSH and TLS for establishing shared secret keys between remote parties.

-----

## Data Encryption for HDCM client

The following points detail the **process behind data encryption for HDCM client:**

1. When creating a data request, the HIU does the following:
	- Creates a set of Elliptic-curve Diffie–Hellman (ECDH) parameters
	- Generates a ECDH key pair (dhsk(U) , dhpk(U)) (which is a short-term public-private key pair)
	- Generates a 32-byte random value, rand(U) which is also called nonce.
2. The HIU sends these values to HDCM, along with the data request via a digitally-signed API call.
3. HDCM forwards the request to the HIP, again via a digitally-signed API call.
4. HIP checks whether the consent artefact is valid, and whether the data being requested is in keeping with the terms of the artefact. If the artefact is valid, the HIP does the following:
	- Generates a fresh ECDH public-private key pair in the same group as specified by the HIU ((dhsk(P), dhpk(P))
		- Generates a 32-byte random value rand(P) aka nonce.
		- Computes a ECDH shared key dhk(U,P) using dhpk(U) and dhsk(P)
		- Computes a 256-bit session key sk(U,P) using dhpk(U) and dhsk(P), which is used to encrypt the data sent from HIP to HIU.
	- HIP sends the public key dhpk(P), the nonce rand(P) and the encrypted data to the HIU.

-----
## Data decryption for HIU

The following process is **applied to decrypt the data that the HIU receives:**

1. HIU receives the encrypted data along with keymaterial containing dhpk(p), nonce.
2. HIU queries through stored data and gets the keymaterial which it created when initiating the data flow request, as follows:
	- It computes a ECDH shared key dhk(U,P) using dhpk(P) and dhsk(U).
	- It then computes a 256-bit session key sk(U,P) using dhpk(P) and dhsk(U), which is used to decrypt the data sent from HIP to HIU.

**Note:**
In order to generate the shared secret key, dhpk(P) should be used, minus headers. Following the big endian (network byte order) keeps the used to derive the shared secret consistent. Also as the cryptography deals with large numbers, it's recommended that no data is converted to binary format until its first converted to big integer. 

Here is a sample set of libraries that you can use:

- Openssl
- Bouncy castle (ensure the X dhpk is a big integer)
- NaCl
- Libgcrypt
- PyNaCls
- TweetNaCl

While most libraries allow exporting of public keys, these keys are compressed and encoded for the most part. It is best to use the libraries to extract the uncompressed form of the public key, that will start with a hex 04. The 32 bytes after the 04 is the X.

The ECDH mechanism ensures that the shared key dh(U,P) can also be computed at the other end by the HIU using the values dhpk(P) (HIP's ECDH public key) and dhsk(U) (HIU's ECDH private key). For this reason, the HIP must ensure that the encrypted data is sent along with dhpk(P) and rand(P). 

The following data flow diagram represents the information encryption and decryption process between the HIU and the HIP:

![encryption-decryption process flow](/abdm-docs/img/ecryption-decryption.png)

## Steps to encrypt data

The following steps are involved in data encryption, on both sides:

The session key is derived from the shared secret key dh(U, P) as follows:

1. XOR the nonce (HIP and HIU)
2. Take the first 20 bytes as the salt for HKDF
3. Derive the key using HKDF(shared key, salt)

Now encrypt the data using AES GCM as follows:

1. XOR the nonce
2. Take the last 12 bytes as the IV for GCM
3. Encrypt the data

**Data encryption summary: Choice of Elliptic-curve Diffie–Hellman parameters**

The key exchange will be performed over Elliptic Curve Cryptography (ECC) groups. We will adhere to a single ECC curve, namely Curve25519, in all encryption operations. Curve25519 is used in ECDH implementations in various protocols like SSH and WhatsApp.

Examples of encryption and decryption using ECDH key exchange:

## For Java

Derived form Fidelius Charm, a magic spell that can conceal secrets.

In the context of projectEka, this is a reference service that does the following

- Generates key Parameters (Private key, Public key and nonce).
- For HIP encrypt given data based on the key parameters passed and give public key in a format that can be shared with the HIU.
- For HIU decrypt the data based on the key parameters passed

**How to run**
- Clone repo ```git clone git@github.com:sukreet/fidelius.git```
- build jar ```./gradlew clean build```
- Run application on port ```java -Dserver.port=8090 -jar build/libs/fidelius-0.0.1-SNAPSHOT.jar```

**Available APIs**

API to generate key material

Request:

```curl --location --request GET 'http://localhost:8090/keys/generate' \ --header 'Accept: application/json' ```

Response:

```{ "privateKey": "CIcMqJzOE+CUpDbkp2WAwfatqppQqiP4q6yOYPYCeBo=", "publicKey": "BECzeFbSDRJTeedGinISJzPdSuC5ZTtniV+XNXAFIwtnNukNnQWcKVOKhJiiGtJc3bfKGXhWOqQZVyQlsSUv8WA=", "nonce": "tBZ0wkJEQJ0rRmkCGF3Utr/ASwydkoGMfUhhl8Nj9r4=" }```

API to Encrypt data (for HIP)

Request:

```curl --location --request POST 'http://localhost:8090/encrypt' \ --header 'Content-Type: application/json' \ --data-raw '{ "receiverPublicKey": "Public key received as a part of data transfer request", "receiverNonce": "Nonce received as a part of data transfer request", "senderPrivateKey": "Private key generated by sender (HIP) using /keys/generate", "senderPublicKey": "Public key generated by sender (HIP) using /keys/generate", "senderNonce": "Nonce key generated by sender (HIP) using /keys/generate", "plainTextData": "valid fhir document" }'```

Response:

```{ "encryptedData": "encrypted FHIR document", "keyToShare": "Public key that needs to be shared with HIU along with encrypeted data" }```

API to decrypt data (for HIU)

Request:

```curl --location --request POST 'http://localhost:8090/decrypt' \ --header 'Content-Type: application/json' \ --data-raw '{ "receiverPrivateKey": "Private key corresponding to the public that was shared whith HIP as part of data request", "receiverNonce": "Nonce that was shared with HIP as part of data request", "senderPublicKey": "public key received from HIP along encrypeted data", "senderNonce": "nonce received from HIP along encrypeted data", "encryptedData": "encrypted FHIR document" }'```

Response:

```{ "decryptedData": "FHIR document" }```

## For Command Line

The core logic for [**Fidelius CLI 59**](https://github.com/mgrmtech/fidelius-cli) has been excerpted from (and improved upon) this [SpringBoot project 14](https://github.com/sukreet/fidelius) (with the same name, which has been used in some form, in the webinar demos).

A few of the core improvements include:

- A CLI implementation, which can be easily integrated into any tech stack without much overhead
- An expansive, well thought-out set of APIs
- The encryption/decryption commands also accept public keys in X509 format
The latest Fidelius CLI release (v1.2.0 as of this writing) can be [downloaded from here](https://github.com/mgrmtech/fidelius-cli/releases)

- You can also find example integrations with NodeJS, Python, and PHP; in the [examples](https://github.com/mgrmtech/fidelius-cli/tree/main/examples) 59 folder inside the [repo.](https://github.com/mgrmtech/fidelius-cli)

- We also have a short video demonstrating Fidelius CLI’s usage in the context of a HIP.

( insert video from Saiki )



