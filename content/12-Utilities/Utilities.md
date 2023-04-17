---
title: "Utilities"
date: 2023-03-07T18:00:04+05:30
Weight: 1
draft: false
pre : "<b>8.1 </b>"
---

{{% notice style="primary" title="Overview " icon="list-alt" %}}
- [Convert Image to Base64](#convert-image-to-base64)
- [RSA Encryption](#rsa-encryption)
{{% /notice %}}

## Convert Image to Base64 
Converting an image into Base64 string means taking the binary representation of an image and converting it into a string of ASCII digits (A-Z, a-z, 0-9).

To convert an image into Base64 :
- use https://codebeautify.org/image-to-base64-converter
- After uploading the image and converting into Base64 string, copy the string and use it in the response body of API which expects it.

#### Sample User Experience for Converting Image to Base64

![convert_image_to_base64](../convert_image_to_base64.gif)


## RSA Encryption
RSA(Rivest-Shamir-Adleman) is an Asymmetric encryption technique that uses two different keys as public and private keys to perform the encryption and decryption. With RSA, you can encrypt sensitive information with a public key and a matching private key is used to decrypt the encrypted message.


To encrypt the data :
- *Step-1:* [API to retrieve public key](#api-to-retrieve-the-public-key)
- *Step-2:* [RSA Encryption via online](#rsa-encryption-via-online-while-using-postman)


#### API to retrieve the public key
Authentication token public certificate. This certificate is also used to encrypt the data.

![retrieve the public key](../retrieve_public_keey_api.png)


**BASE URL:** https://healthidsbx.abdm.gov.in/api

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="GET /v1/auth/cert$" >}}

#### RSA Encryption via online (while using Postman)

https://www.devglan.com/online-tools/rsa-encryption-decryption

After encrypting, copy the string and use it in the response body of API which expects it.

#### Sample User Experience for RSA Encryption
![rsa_encryption_flow](../process-flow.gif)



