+++
title = "Implementation Principles"
date = 2023-04-13T05:10:00+05:30
weight = 1
chapter = true
pre = "<b>3.8.1 </b>"
+++

# Encryption/Decryption Implementation Principles

The following **abbreviations** are used in this section:

-   ECDH: Elliptic-curve Diffie–Hellman Key Exchange
-   AES-GCM: Advanced Encryption Standard-Galois/Counter Mode
-   DHK(U,P): Elliptic-curve Diffie–Hellman Key
-   P and U (for Provider, and User) are annotations for the involved systems
-   DHPK: Elliptic-curve Diffie–Hellman public key
-   DHSK: Elliptic-curve Diffie–Hellman secret/private key
-   RAND: Random String
-   HKDF: Hash-based Key Derivation Function
-   HIP: Health Information Provider
-   HIU: Health Information User
-   HDCM: Health Data Consent Manager

Information shared as part of the data flow will be **secured using an encryption mechanism that ensures perfect forward secrecy.**

This means that even if any of the key materials stored at HIPs, HIUs or HDCM clients (either long-term private keys or session keys) are compromised, it would not be possible to decipher data that was previously exchanged.

The encryption mechanism uses **Elliptic-curve Diffie–Hellman Key Exchange (ECDH),** which is used in many Internet protocols such as SSH and TLS for establishing shared secret keys between remote parties.

---

## Data Encryption at HIP (for HDCM client)

The following points detail the **process behind data encryption for HDCM client:**

1. When creating a data request, the HIU does the following:
    - Creates a set of Elliptic-curve Diffie–Hellman (ECDH) parameters
    - Generates a ECDH key pair (DHSK(U) , DHPK(U)) (which is a short-term public-private key pair)
    - Generates a 32-byte random value, RAND(U) which is also called nonce.
2. The HIU sends these values to HDCM, along with the data request via a digitally-signed API call.
3. HDCM forwards the request to the HIP, again via a digitally-signed API call.
4. HIP checks whether the consent artefact is valid, and whether the data being requested is in keeping with the terms of the artefact. If the artefact is valid, the HIP does the following:
    - Generates a fresh ECDH public-private key pair in the same group as specified by the HIU (DHSK(P), DHPK(P))
        - Generates a 32-byte random value RAND(P) aka nonce.
        - Computes a ECDH shared key DHK(U,P) using DHPK(U) and DHSK(P)
        - Computes a 256-bit session key SK(U,P) using DHPK(U) and DHSK(P), which is used to encrypt the data sent from HIP to HIU.
    - HIP sends the public key DHPK(P), the nonce RAND(P) and the encrypted data to the HIU.

---

## Data Decryption for HIU

The following process is **applied to decrypt the data that the HIU receives:**

1. HIU receives the encrypted data along with keymaterial containing DHPK(p), nonce.
2. HIU queries through stored data and gets the keymaterial which it created when initiating the data flow request, as follows:
    - It computes a ECDH shared key DHK(U,P) using DHPK(P) and DHSK(U).
    - It then computes a 256-bit session key SK(U,P) using DHPK(P) and DHSK(U), which is used to decrypt the data sent from HIP to HIU.

---

The ECDH mechanism ensures that the shared key DHK(U,P) can also be computed at the other end by the HIU using the values DHPK(P) (HIP's ECDH public key) and DHSK(U) (HIU's ECDH private key). For this reason, the HIP must ensure that the encrypted data is sent along with DHPK(P) and RAND(P).

**Data encryption summary: Choice of Elliptic-curve Diffie–Hellman parameters**

The key exchange is performed over Elliptic Curve Cryptography (ECC) groups. All encryption/decryption operations adhere to a single ECC curve, namely Curve25519. Curve25519 is used in ECDH implementations in various protocols like SSH and WhatsApp.

---

## Steps to encrypt/decrypt data, in brief

The following data flow diagram represents the information encryption and decryption process between the HIU and the HIP:

![encryption-decryption process flow](/abdm-docs/img/ecryption-decryption.png)

The following steps are involved in data encryption (and also decryption):

The session key is derived from the shared secret key DHK(U, P) as follows:

1. XOR the nonce (HIP and HIU)
2. Take the first 20 bytes as the salt for HKDF (Hash-based Key Derivation Function)
3. Derive the session key using HKDF(shared key, salt)

Now encrypt the data using AES GCM as follows:

1. XOR the nonce
2. Take the last 12 bytes as the IV for GCM
3. Encrypt/Decrypt the data

Example implementation code (in Java) for the above steps can be found below:

-   [Encryption](https://github.com/mgrmtech/fidelius-cli/blob/main/src/main/java/com/mgrm/fidelius/encryption/EncryptionController.java)
-   [Decryption](https://github.com/mgrmtech/fidelius-cli/blob/main/src/main/java/com/mgrm/fidelius/decryption/DecryptionController.java)
