---
title: "Retrieve ABHA via Mobile OTP"
date: 2022-05-07T18:00:04+05:30
weight: 2
draft: false
---


## Retrieve ABHA via Mobile OTP

## Overview of the functionality 

- To retrieve ABHA (Health ID), an OTP is sent on mobile number along with the user's demographic detail.
- User's health ID is retrieved from the ABDM server.

## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![Login ABHA ID via Aadhaar Otp](/abdm-docs/img/Forgot_ABHA(Health_ID)_Retrieve_via_Mobile_OTP.png)


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

**Response:** 200 OK

```json
{
    "accessToken": "string",
    "expiresIn": 600,
    "refreshExpiresIn": 1800,
    "refreshToken": "string",
    "tokenType": "bearer"
}
```



**2. Generate Mobile OTP as part of Forgot flow**

Explanation - API accepts Mobile Number and then generates OTP for it.

Request Body - Required

Responce - API Accepts Mobile Number and then generates OTP for it. Returns Transaction ID.

**URL:** https://healthidsbx.abdm.gov.in/api/v1/forgot/healthId/mobile/generateOtp

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

generateOtpRequest  (body)

```json
{
  "mobile": "9545812125"
}
```

**Response:** 200  OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```



**3. Verify Mobile OTP sent as part of forget ABHA number**

Explanation - API accepts OTP and then checks is it Valid as per given Mobile Transaction.

Request Body - Required

Response - API accepts OTP then returns ABHA Number accordingly.

**URL:** https://healthidsbx.abdm.gov.in/api/v1/forgot/healthId/mobile

**Need to check API in pdf it is mentioned as v1/forgot/healthId/aadhaar **

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

retriveHealthIdMobilePayLoad  (body)

```json
{
  "dayOfBirth": "31",
  "firstName": "Kishan",
  "gender": "M",
  "lastName": "Singh",
  "middleName": "kumar",
  "monthOfBirth": "05",
  "name": "kishan kumar singh",
  "otp": "816406",
  "status": "Active",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "yearOfBirth": "1995"
}
```

**Response:** 200  OK

```json
{
  "healthId": "deepak.pant",
  "healthIdNumber": "43-4221-5105-6749",
  "jwtResponse": null
}
```


## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Retrieve_ABHA_Via_Mobile_Otp.json)

**Download the Curls** [here](/abdm-docs/Curls/)



