+++
title = "Encryption & Decryption"
date = 2023-04-11T05:10:00+05:30
weight = 8
chapter = true
pre = "<b>3.8 </b>"
+++

# Encryption and Decryption

The aim of encryption is to ensure that only the party (HIU) that has been granted consent by the user (or patient) is able to access the health data information of the user.

Here's at a high level how the **process of encyption and decryption** works between HIUs and the HRP/HIP, with the consent of the patient:

1. Every Health Information User (HIU) has 2 keys; that is public & private key.
2. When the HIU wants to request for any HIP/HRP for information, the public key of the HIU is shared in the request.
3. The HIP/HRP validates that the user/patient has granted consent to the HIP (requesting for data) to share health data information.
4. Once that is validated, the HIP/HRP will encrypt the data with the Public Key of the HIU
5. The ecnrypted data is then shared with HIU.
6. HIUs will have to decrypt data using their Private key.

Here's a **sequence diagram** to understand the how the flow and exchange of information takes place:

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
HIU System->>Gateway:Request for Health Data
Gateway->>HIP Repository:Forward request with encrypted HIU Public key<br/>POST/health-information/hip/request
activate HIP Repository
HIP Repository-->>HIP System:notification
HIP Repository->>Gateway:POST/health-information/hip/on-request
Note over HIP Repository,HIP System:Prepare data (encryption)
HIP Repository-->>HIU System: Direct data transfer<br/>POST/datapush-url
HIP Repository->>Gateway:Notify on the transfer<br/>POST/health-information/notify
{{< /mermaid >}}


## Examples of encryption and decryption using ECDH key exchange

If you are using one of these languages, it will be quicker if you use the following examples for reference. 

1. [For Java](/abdm-docs/3-milestone2/encryption-decryption/java/index.html)
2. [For Command Line](/abdm-docs/3-milestone2/encryption-decryption/command-line/index.html)
3. [For C#](/abdm-docs/3-milestone2/encryption-decryption/for-c-hash/index.html)
4. [For New Programming Language](/abdm-docs/3-milestone2/encryption-decryption/new-prog-language/index.html)