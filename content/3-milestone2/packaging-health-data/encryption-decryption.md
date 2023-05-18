+++
title = "Encryption and Decryption"
date = 2023-05-18T05:10:00+05:30
weight = 3
chapter = true
pre = "<b>3.7.3 </b>"
+++

# Data Encryption and Decryption

The following abbreviations are used in this section:

- ECDH: Elliptic-curve Diffie–Hellman Key Exchange
- AES-GCM: Advanced Encryption Standard-Galois/Counter Mode
- DHPK: Elliptic-curve Diffie–Hellman public key
- DHSK: Elliptic-curve Diffie–Hellman secret/private key
- P and U is annotation for system
- DHK(U,P): Elliptic-curve Diffie–Hellman Key
- Rand: Random String

Information shared as part of the data flow will be secured using an encryption mechanism that ensures perfect forward secrecy. This means that even if any of the key materials stored at HIPs, HIUs or HDCM clients (either long-term private keys or session keys) are compromised, it would not be possible to decipher data that was previously exchanged. The encryption mechanism uses Elliptic-curve Diffie–Hellman Key Exchange (ECDH), which is used in many Internet protocols such as SSH and TLS for establishing shared secret keys between remote parties.

---

## Data encryption for HDCM client

The following points detail the process behind data encryption for HDCM client:

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

---

## Data decryption for HIU

The following process is applied to decrypt the data that the HIU receives:

1. HIU receives the encrypted data along with keymaterial containing dhpk(p), nonce.
2. HIU queries through stored data and gets the keymaterial which it created when initiating the data flow request, as follows:
	- It computes a ECDH shared key dhk(U,P) using dhpk(P) and dhsk(U).
	- It then computes a 256-bit session key sk(U,P) using dhpk(P) and dhsk(U), which is used to decrypt the data sent from HIP to HIU.

**Note:**

In order to generate the shared secret key, dhpk(P) should be used, minus headers. Following the big endian (network byte order) keeps the used to derive the shared secret consistent. Also as the cryptography deals with large numbers, it's recommended that no data is converted to binary format until its first converted to big integer. Here is a sample set of libraries that you can use:

- Openssl
- Bouncy castle (ensure the X dhpk is a big integer)
- NaCl
- Libgcrypt
- PyNaCl
- TweetNaCl

While most libraries allow exporting of public keys, these keys are compressed and encoded for the most part. It is best to use the libraries to extract the uncompressed form of the public key, that will start with a hex 04. The 32 bytes after the 04 is the X.

The ECDH mechanism ensures that the shared key dh(U,P) can also be computed at the other end by the HIU using the values dhpk(P) (HIP's ECDH public key) and dhsk(U) (HIU's ECDH private key). For this reason, the HIP must ensure that the encrypted data is sent along with dhpk(P) and rand(P). The following data flow diagram represents the information encryption and decryption process between the HIU and the HIP:

![Encryption and Decryption Process Between HIU and HIP](../packaging-encryption-decryption.png)

**Steps to encrypt data**

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

For Java example, see [here.](https://github.com/sukreet/fidelius/tree/84bc68c8a80d91a665dd88b05e5757a09a2d663a/src/main/java/in/projecteka/fidelius)
For C# example, see [here.](https://gist.github.com/Nexengineer/23589d0e8eeab0ad0f50cffdf4be6bca)
For NodeJS, Python, Ruby and PHP example see [here.](https://devforum.abdm.gov.in/t/fidelius-cli-a-complete-end-to-end-cryptography-solution/3906)





