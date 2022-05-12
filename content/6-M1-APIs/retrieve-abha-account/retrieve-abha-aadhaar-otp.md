---
title: "Retrieve ABHA via Aadhaar OTP"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---


## Retrieve ABHA via Aadhaar OTP

## Overview of the functionality 

- To retrieve ABHA (Health ID), an OTP is sent on a registered mobile number and the user's health ID is retrieved from the ABDM server.
- The sequence of APIs used via this method is shown in the diagram below. 

## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![Login ABHA ID via Aadhaar Otp](/abdm-docs/img/Forgot_ABHA(Health_ID)_Retrieve_via_Aadhaar_OTP.png)


## API Information Request Response 


1. Api Accepts Aadhaar and then creates OTP for linked Mobile number

**URL:** https://healthidsbx.ndhm.gov.in/api/v2/forgot/healthId/aadhaar/generateOtp

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

aadharNumberWebOptionalRequestPayload  (body)

```json
{
  "aadhaar": "afcmKRGLmMtGiG701dEXOBY7k0e94Cc+Cknx88lrkOa6uxQbMwDZWnlp2PUsw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0Ftj2Qb6uEbuDrqQ4BxN33TG561vCbdkh9MoV2nKckOJhdoBy7shjXJSfiRZf0d9DWOot4zlsBD03H6wx94m51Qh+pCGLQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI="
}
```

**Response:** 200 OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```



2. Api Accepts OTP and then Checks is it valid for given Transaction

**URL:** https://healthidsbx.ndhm.gov.in/api/v2/forgot/healthId/aadhaar

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

authAccountAadhaarOTPWebRequest  (body)

```json
{
  "otp": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI=",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
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



