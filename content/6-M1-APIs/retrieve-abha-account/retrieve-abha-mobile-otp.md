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


1. Api Accepts Mobile Number and then generates OTP for it to Start Registration

**URL:** https://healthidsbx.ndhm.gov.in/api/v2/forgot/healthId/mobile/generateOtp

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

generateOtpRequest  (body)

```json
{
  "mobile": 9545812125
}
```

**Response:** 200 OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```



2. Api Accepts OTP and then checks is it Valid as per given Mobile Transaction

**URL:** https://healthidsbx.ndhm.gov.in/api/v2/forgot/healthId/mobile

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

retriveHealthIdMobilePayLoad  (body)

```json
{
  "dayOfBirth": 31,
  "firstName": "Kishan",
  "flow": "RETRIEVE_HID",
  "gender": "M",
  "lastName": "Singh",
  "middleName": "kumar",
  "monthOfBirth": "05",
  "name": "kishan kumar singh",
  "otp": 816406,
  "status": "Active",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "yearOfBirth": 1995
}
```

**Response:** 200 OK

```json
{
  "healthId": "deepakndhm",
  "healthIdNumber": "43-4221-5105-6749",
  "jwtResponse": {
    "expiresIn": 1800,
    "refreshExpiresIn": 86400,
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
  }
}
```


## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)



