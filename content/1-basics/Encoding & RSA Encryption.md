---
title: "Encoding & RSA Encryption"
date: 2022-05-07T18:00:04+05:30
Weight: 9
draft: false
pre : "<b>1.9 </b>"
---


{{% notice style="primary" title="Overview " icon="list-alt" %}}
Several API parameters require encoding / encryption. This section points you to tools that are useful when testing APIs using POSTMAN

- [Convert Image to Base64](#convert-image-to-base64)
- [RSA Encryption](#rsa-encryption)
{{% /notice %}}

## Convert Image to Base64 
Converting an image into Base64 string means taking the binary representation of an image and converting it into a string of ASCII digits (A-Z, a-z, 0-9).

To convert an image into Base64 :
- use https://codebeautify.org/image-to-base64-converter
- After uploading the image and converting into Base64 string, copy the string and use it in the request body of API which expects it.

#### Sample User Experience for Converting Image to Base64

![convert_image_to_base64](../convert_image_to_base64.gif)


## RSA Encryption
RSA(Rivest-Shamir-Adleman) is an Asymmetric encryption technique that uses two different keys as public and private keys to perform the encryption and decryption. With RSA, you can encrypt sensitive information with a public key and a matching private key is used to decrypt the encrypted message.


To encrypt the data :
- *Step-1:* [API to retrieve public key](#api-to-retrieve-the-public-key)
- *Step-2:* [RSA Encryption via online](#rsa-encryption-via-online-while-using-postman)

{{% notice title="RSA Encryption" %}}
API Type|Certificate URL|Cipher Type
|--|----|------|
[For V3 APIs](#rsa-encryption-for-v3-apis)|https://healthidsbx.abdm.gov.in/api/v1/auth/cert|RSA/ECB/OAEPWithSHA-1AndMGF1Padding
[For PHR V1 APIs](#rsa-encryption-for-phr-v1-apis)|https://phrsbx.abdm.gov.in/api/v1/phr/public/certificate | RSA/ECB/PKCS1Padding
[For V1 APIs](#rsa-encryption-for-v1-apis)|https://healthidsbx.abdm.gov.in/api/v1/auth/cert | RSA/ECB/PKCS1Padding
[For V2 APIs](#rsa-encryption-for-v2-apis)|https://healthidsbx.abdm.gov.in/api/v2/auth/cert | RSA/ECB/PKCS1Padding

{{% /notice %}}

## RSA Encryption For V3 APIs

### API to retrieve the public key
Authentication token public certificate. This certificate is also used to encrypt the data.

![retrieve the public key](../retrieve_public_keey_api.png)


**BASE URL:** https://healthidsbx.abdm.gov.in/api

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="GET /v1/auth/cert$" >}}

### RSA Encryption via online (while using Postman)

https://www.devglan.com/online-tools/rsa-encryption-decryption

**Select cipher type - RSA/ECB/OAEPWithSHA-1AndMGF1Padding**

![retrieve the public key](../cipher_type.png)

After encrypting, copy the string and use it in the response body of API which expects it.


## RSA Encryption For PHR V1 APIs

### API to retrieve the public key


![retrieve the public key](../public_certificate_for_other_api.png)


**BASE URL:** https://phrsbx.abdm.gov.in/

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="GET /v1/phr/public/certificate$" >}}

### RSA Encryption via online (while using Postman)

https://www.devglan.com/online-tools/rsa-encryption-decryption

**Select cipher type - RSA/ECB/PKCS1Padding**

![retrieve the public key](../cipher_type_others.png)

After encrypting, copy the string and use it in the response body of API which expects it.


## RSA Encryption For V1 APIs

### API to retrieve the public key


![retrieve the public key](../v1_api.png)

**BASE URL:** https://healthidsbx.abdm.gov.in/api

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="GET /v1/auth/cert$" >}}

### RSA Encryption via online (while using Postman)

https://www.devglan.com/online-tools/rsa-encryption-decryption

**Select cipher type - RSA/ECB/PKCS1Padding**

![retrieve the public key](../cipher_type_others.png)

After encrypting, copy the string and use it in the response body of API which expects it.


## RSA Encryption For V2 APIs

### API to retrieve the public key


![retrieve the public key](../v2_api.png)

**BASE URL:** https://healthidsbx.abdm.gov.in/api

{{< swaggermin src="/abdm-docs/Yaml/abdm-abha-service-1_0.yml" api="GET /v2/auth/cert$" >}}

### RSA Encryption via online (while using Postman)

https://www.devglan.com/online-tools/rsa-encryption-decryption

**Select cipher type - RSA/ECB/PKCS1Padding**

![retrieve the public key](../cipher_type_others.png)

After encrypting, copy the string and use it in the response body of API which expects it.


#### Sample User Experience for RSA Encryption
![rsa_encryption_flow](../rsa_encryption.gif)



