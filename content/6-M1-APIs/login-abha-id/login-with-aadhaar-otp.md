---
title: "Login with Aadhaar OTP"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---

## Login with Aadhaar OTP

## Overview of the functionality 

- An OTP is triggered with the Aadhaar linked mobile number of the patient. 
- The patient must provide the OTP to the user to complete the authentication


## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![Login ABHA ID via Aadhaar Otp](/abdm-docs/img/Login_With_ABHA_using_mobile.png)



## API Information Request Response 

1. Authentication token public certificate. This certificate is also used to encrypt the data.

**URL:** https://healthidsbx.abdm.gov.in/api/v1/auth/cert

**Request:** GET  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)


**Body:**

```json

```

**Response:** 200

string



2. Search a user by ABHA Number or ABHA Address.

This API returns only Active or Deactive ABHA Number/ Address (Never returns Permanently Deleted ABHA Number/ Address)

Explanation - API checks ABHA Number or ABHA Address to find User.

Request Body - Required. Here healthId attribute means ABHA Address

Response - API checks ABHA Number or ABHA Address to find User. API returns only Active or Deactive ABHA Number/ Address (Never returns Permanently Deleted ABHA Number/Address)

**URL:** https://healthidsbx.abdm.gov.in/api/v1/search/searchByHealthId

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID  string (header)


**Body:**

searchRequest (body)

```json
{
  "healthId": "deepak.pant"
}
```

**Response:** 200

```json
{
  "authMethods": [
    "AADHAAR_OTP"
  ],
  "healthId": "deepakndhm",
  "healthIdNumber": "43-4221-5105-6749",
  "name": "kishan kumar singh",
  "status": "ACTIVE"
}
```


3. Initiate authentication process for given Health ID

**URL:** https://healthidsbx.abdm.gov.in/api/v1/auth/init

**NEED to check actual API is v2/auth/init in pdf document provided**

**Request:** GET  

**Parameters:**

- Authorization string (header)

- X-HIP-ID  string (header)


**Body:**

authRequest  (body)

```json
{
  "authMethod": "AADHAAR_OTP",
  "healthid": "43-4221-5105-6749"
}
```

**Response:** 200

```json
{
  "mobileNumber": "XXXXXX2125",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```


4. Authentication with Aadhaar OTP based auth transaction

**URL:** https://healthidsbx.abdm.gov.in/api/v1/auth/confirmWithAadhaarOtp

**Request:** POST  

**Parameters:**

authAccountAadhaarOTPRequest  (body)

- Authorization  string (header)

- X-HIP-ID  string (header)


**Body:**

```json
{
  "otp": "816406",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200

```json
{
  "expiresIn": 1800,
  "refreshExpiresIn": 86400,
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
}
```



## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)



