---
title: "Deactivate ABHA via Mobile Otp"
date: 2022-05-07T18:00:04+05:30
weight: 2
draft: false
---

# Deactivate ABHA via Mobile Otp


## Overview of the functionality 

- Users may De-activate his/her ABHA (Health ID)

Following will happen (during the deactivation period) if you deactivate your ABHA (Health ID) :

1. You will lose access to all ABDM applications.
2. You will no longer be able to share your health records over the ABDM network.
3. You will no longer be able to share your ABHA (Health ID) at any health facility.


## API Sequence 

The sequence of APIs used via this method is shown in the diagram below.

![Deactivate ABHA via Mobile Otp](/abdm-docs/img/De-Activate_ABHA(Health_ID).png)


## API Information Request Response 




**1. Generate the Gateway session**

Bearer token is received as part of respose and should be passed a Authorization token for subsequent API calls.

**URL:** https://dev.ndhm.gov.in/gateway/v0.5/sessions

**Request:** POST  

**Body:**

```json
{
    "clientId": "your-clientID",
    "clientSecret": "your-clientSecret",
    "grantType": "client_credentials"
}
```

**Response:** 200   OK

```json
{
    "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJBbFJiNVdDbThUbTlFSl9JZk85ejA2ajlvQ3Y1MXBLS0ZrbkdiX1RCdkswIn0.eyJleHAiOjE2NTMzNjkyNTYsImlhdCI6MTY1MzM2ODY1NnR",
    "expiresIn": 600,
    "refreshExpiresIn": 1800,
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICIyMWU5NzA4OS00ZTcxLTQyNGEtOTAzYS1jOTAyMWM1NmFlNWYifQ.eyJleHAiOjE2NTMzNzA0NTYsImlhdCI6MTY1MzM2ODY1NiwianRpIjoi",
    "tokenType": "bearer"
}
```



\
\
\
**2. Authentication token public certificate. This certificate is also used to encrypt the data.**

**URL:** https://healthidsbx.abdm.gov.in/api/v1/auth/cert

**Request:** GET  

**Parameters:**

- Authorization : Access token which was issued after successful login with gateway auth server

string (header)

- X-HIP-ID : Identifier of the health information provider to which the request was intended

string (header)


**Response:** 200   OK


```text

-----BEGIN PUBLIC KEY-----
M3IdPoUuNUNUYv33QrHIb1Nmh6TECSbmokLCsPx0hHYCsH37FIDE7fXKWNXYSjtRLBF2vwt7y8qUTdklfCLmO
VqVXacyMslKaXzsbYxHaAsm9Dkp6A0oprgnPL9x0/g9AC1/n90GakXWAdnZr6Jh/tfmjAeU+On1M6qSo1fTvH
ppHKIzs/XdLWq7j2ENdNNWd7qHSa1MIYjCSJmO/zCRl7S/V3bvibAsXWRLamfqcNw8E+IuhQc/PK4khuHsp80
N4RjUI1D5u84I0Qxn4G10i/gsU4Hls2RZODmOfxBBGjjgv7tO1HMa7BLyRx2NxFRCQ7d1vN6eQnxIzEFPfRyF
yoMKpctbUS0kfwYI0T1sT6UidgDV2//SVv0ymZgeSYKwdPT2LC4HzJhpOvYMVsyGq6aEA5ieUp4wxOs8Ab3pQ
zJKuTdXBRZo18jGoj3ZT4fGRZ/NfWrkGZiKR1SSOYZeb0MrQZnz2Or0C//fiIzpfW6AeYMd+2nUAjX+I+K2xR
tVfSxys4I8Ylt3R3jdeVb+nlQaU6hCVlaWW1UXiljh8asnpj6q1qXPB8RoSUVIwsiCcQVibaY4OuFd6EHOgnO
ZIMGomLoDz7omTrmpOn+dobCa7yDvkNGPjoUr67RVq0hpJ9pVJVNL9INJfK5SPXJxUqEilkVTgph0FeoObvHVXnw=
-----END PUBLIC KEY-----

```



\
\
\
**3. Generate Mobile OTP to start mobile txn.**

Explanation - Api Accepts Auth Token and Generates OTP on mobile number.

Request Body - Required

Responce - Api Accepts Auth Token and Generates OTP on mobile number. Returns Error for Unauthorized token .

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/mobile/generateOTP

**Request:** POST  

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

- X-HIP-ID string (header) : your-HIP-ID

- X-Token string (header) : Bearer your-X-token



**Response:** 200   OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```



\
\
\
**4. Deactivate the account using mobile otp.**

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/profile/deactivate

**Request:** POST  

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

- X-HIP-ID string (header) : your-HIP-ID

- X-Token string (header) : Bearer your-X-token


**Body:**

deactivateAccountByOtpWebRequest  (body)

```json
{
  "authMethod": "MOBILE_OTP",
  "otp": "OISH0Ck8M4XFh7XggpLmBnyNdXD2qbMSShJERkHx8wLn+omotRxU5LXyspe0qL3v2OgOsdiw/bVMtHr/FcKHbopRga+eD1d+3tfI63qS/zosy45GYmvbBU4dVGMAbRzmYCR7gJIlxfRl2X5V9nD3rKLBL6n3s5lHn6OAW6R9lP5uSaFKRu8W30BnptSArWvGHxXlZPKogm9vezKWGRkjP1aiFlyRWYpqyqmM2r7w88atALyO0F0e98a9s4jzVZ1ggpip/3+awNTZMsL/F9Vxx0kuKayVSGiGunTO+aVRvIsM6j8zN5vSvqfi5W7v8a4I0takq3V+hCGi8EncKPGFopqXvATn/I59HhgoUPXNNZbWpDgQ+BLxXqb0G1tyQCegQe/g",
  "reasons": ["205"],
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 204




## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Deactivate_ABHA_Via_Mobile_Otp.json)

**Download the Curls** [here](/abdm-docs/Curls/)


