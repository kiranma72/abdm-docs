+++
title = "Encryption & Decryption"
date = 2023-04-11T05:10:00+05:30
weight = 8
chapter = true
pre = "<b>3.8 </b>"
+++

# Encryption and Decryption

The aim of encryption is to ensure that only the party (HIU) that has been granted consent by the user (or patient) is able to access the health data information of the user.

Here's a high level overview on how the **process of encyption and decryption** works between HIUs and the HIPs, with the consent of the patient:

1. Every Health Information User (HIU) has 2 keys; that is public & private key.
2. When the HIU wants to request any HIP for information, the public key of the HIU (along with other key material pertaining to the HIU and the corresponding request) is shared in the request.
3. The HIP validates that the user/patient has granted consent to the HIP (requesting for data) to share health data information.
4. Once that is validated, the HIP will encrypt the data using a shared key (which is generated using HIP's private key, and HIU's publick key material)
5. The encrypted data is then shared with HIU, along with the public key of HIP (and other key material).
6. HIUs will have to decrypt data using a shared key (which is generated using HIU's private key, and HIP's publick key material).

Here's a **sequence diagram** to understand the how the flow and exchange of information takes place:

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
HIU System->>Gateway:Request for Health Data
Gateway->>HIP Repository:Forward request with HIU public key material<br/>POST/health-information/hip/request
activate HIP Repository
HIP Repository-->>HIP System:notification
HIP Repository->>Gateway:POST/health-information/hip/on-request
Note over HIP Repository,HIP System:Prepare data (encryption)
HIP Repository-->>HIU System: Direct data transfer with HIP public key material<br/>POST/datapush-url
HIP Repository->>Gateway:Notify on the transfer<br/>POST/health-information/notify
{{< /mermaid >}}

A detailed coverage on the implemetation principles can be found in [this section](/abdm-docs/3-milestone2/encryption-decryption/implementation-principles/index.html).

---

## Example Implementation(s)

The use of Fidelius CLI is encouraged for implementing encryption and decryption as a part of Milestone 2 and Milestone 3 (Building HIP and Building HIU) requirements.

Fidelius CLI's usage is covered in detail in [this section](/abdm-docs/3-milestone2/encryption-decryption/fidelus-cli/index.html).

Following is a short video demonstrating Fidelius CLI’s usage in the context of a HIP.

{{< youtube id="iDcCP9h5hZs" >}}

[**This webinar**](https://youtu.be/rSir2gbkEmk?t=9232) (from 2:33:52) — also covers the usage of Fidelius CLI in detail, from both the HIP and HIU perspectives.

**Using Fidelius CLI with other Programming Languages**

While Fidelius CLI is a Java implementation, the [**`./examples` folder**](https://github.com/mgrmtech/fidelius-cli/tree/main/examples) in the [**corresponding repository**](https://github.com/mgrmtech/fidelius-cli) can be perused for guidance on integrating Fidelius CLI (achieved by invoking the binary as a subprocess) in Node JS, Python, Ruby, and PHP codebases.

1. [NodeJS](https://github.com/mgrmtech/fidelius-cli/blob/main/examples/node/index.js)
2. [Python](https://github.com/mgrmtech/fidelius-cli/blob/main/examples/python/main.py)
3. [Ruby](https://github.com/mgrmtech/fidelius-cli/blob/main/examples/ruby/main.rb)
4. [PHP](https://github.com/mgrmtech/fidelius-cli/blob/main/examples/php/index.php)

The above examples can be run using the following commands:

```
$ node examples/node/index.js
$ python3 examples/python/main.py
$ ruby examples/ruby/main.rb
$ php examples/php/index.php
```
