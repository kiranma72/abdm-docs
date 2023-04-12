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

![Login ABHA via Aadhaar Otp](/abdm-docs/img/Login_With_ABHA.png)



## API Information Request Response 


**1. Generate the Gateway session**

Bearer token is received as part of respose and should be passed a Authorization token for subsequent API calls.

**URL:** https://dev.ndhm.gov.in/gateway/v0.5/sessions

**Request:** POST  

**Body:**

```json
{
    "clientId": "string",
    "clientSecret": "string",
    "grantType": "client_credentials"
}
```

**Response:** 200  OK

```json
{
    "accessToken": "string",
    "expiresIn": 600,
    "refreshExpiresIn": 1800,
    "refreshToken": "string",
    "tokenType": "bearer"
}
```



**2. Authentication token public certificate. This certificate is also used to encrypt the data.**

**URL:** https://healthidsbx.abdm.gov.in/api/v1/auth/cert

**Request:** GET  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)


**Response:** 200  OK

string



**3. Search a user by ABHA Number or ABHA Address.**

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

**Response:** 200  OK

```json
{
    "healthId": "deepak.pant@sbx",
    "healthIdNumber": "12-3456-7890-1234",
    "name": "string",
    "status": "ACTIVE",
    "authMethods": [
        "AADHAAR_BIO",
        "AADHAAR_OTP",
        "DEMOGRAPHICS",
        "PASSWORD",
        "MOBILE_OTP"
    ],
    "tags": null
}
```



**4. Initiate authentication process for a given ABHA Number**

**URL:** https://healthidsbx.abdm.gov.in/api/v2/auth/init

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID  string (header)


**Body:**

authRequest  (body)

```json
{
  "authMethod": "AADHAAR_OTP",
  "healthid": "12-3456-7890-1234"
}
```

**Response:** 200  OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```



**5. Authentication with Aadhaar OTP based auth transaction**

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

**Response:** 200  OK

```json
{
    "token": "string",
    "expiresIn": 1800,
    "refreshToken": "string",
    "refreshExpiresIn": 432000
}
```



## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Login_ABHA_Via_Aadhaar_Otp.json)

**Download the Curls** [here](/abdm-docs/Curls/)



