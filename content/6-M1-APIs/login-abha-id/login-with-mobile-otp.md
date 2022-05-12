---
title: "Login with Mobile OTP"
date: 2022-05-07T18:00:04+05:30
weight: 2
draft: false
---

## Login with Mobile OTP

## Overview of the functionality 

- An OTP is sent to the patient’s mobile number that is linked with the Health ID.
- The patient must share the OTP with the user for verification.
- A token has been returned and can be used for Profile APIs purpose.


## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![Login ABHA ID via Aadhaar Otp](/abdm-docs/img/Login_With_ABHA_using_mobile.png)



## API Information Request Response 

1. Auth token public key

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/auth/cert

**Request:** GET  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)


**Body:**

```json

```

**Response:** 200 OK

```json
string
```

2. Search a user by Health ID Number

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/search/searchByHealthId

**Request:** POST  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)


**Body:**

```json
{
  "healthId": "string"
}
```

**Response:** 200 OK

```json
{
  "authMethods": [
    "AADHAAR_OTP"
  ],
  "healthId": "string",
  "healthIdNumber": "string",
  "name": "string",
  "tags": {
    "additionalProp1": "string",
    "additionalProp2": "string",
    "additionalProp3": "string"
  }
}
```


3. Initiate authentication process for given Health ID

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/auth/init

**Request:** GET  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)


**Body:**

```json
{
  "authMethod": "AADHAAR_OTP",
  "healthid": "string"
}
```

**Response:** 200 OK

```json
{
  "txnId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```


4. Authentication with Mobile OTP based auth transaction

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/auth/confirmWithMobileOTP

**Request:** POST  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)


**Body:**

```json
{
  "otp": "string",
  "txnId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```

**Response:** 200 OK

```json
{
  "token": "string"
}
```



## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)


