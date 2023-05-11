---
title: "Reactivate ABHA via Mobile OTP"
date: 2022-05-07T18:00:04+05:30
weight: 2
draft: false
---

## Overview of the functionality 

- Users may Reactivate his/her ABHA (Health ID) via Mobile OTP by using the below endpoints.



## API Sequence 



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

**Response:** 200 OK

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

- Authorization string (header) : Bearer your-access-token-from-gateway-session

- X-HIP-ID string (header) : your-HIP-ID


**Response:** 200  OK


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
**3. Initiate authentication for reactivation of ABHA (Health ID)**

**URL:** https://healthidsbx.abdm.gov.in/api/v2/auth/reactivate/init

**Request:** POST  

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

- X-HIP-ID string (header) : your-HIP-ID


**Body:**

authRequest  (body)

```json
{
  "authMethod": "MOBILE_OTP",
  "healthid": "43-4221-5105-6749"
}
```

**Response:** 200   OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```



\
\
\
**4. Confirm reactivation txn with mobile otp**

**URL:** https://healthidsbx.abdm.gov.in/api/v2/auth/reactivate

**Request:** POST  

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

- X-HIP-ID string (header) : your-HIP-ID


**Body:**

reactivateByOTPWebRequest  (body)

```json
{
  "authMethod": "MOBILE_OTP",
  "otp": "l+IEVKwPsaKuAYsJOvo1a892uUL+y1Is4GRMQei4sKDI8fVgEBrK6kCu2srUqqvTIq7K0xGfazO7SRlEYclZmqsQoBFm5yhRWjblSn1AMuLLoBlRdqPoVjX8OlZNOb3qKw49uL4lnmZwAAJlIqIkpNnBdAo1XFlNZoZa0UZTdE+2vfJNrUaqvHLAyZ9",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200   OK

```json
{
    "token": "eyJhbGciOiJSUzUxMiJ9.eyJzdWIiOiIzMS0xNzM3LTUyMzUtNzEzNSIsImNsaWVudElkIjoiaGVhbHRoaWQtYXBpIiwic3lzdGVtIjoiQUJIQS1OIiwibW9iaWxlIjoiNzc5OTE1NDk5OCIsImV4cCI6MTY1MzQ2MTU5NiwiaGVhbHRoSWROdW1iZXIiOiIzMS0xNzM3LTUyMzUtNzEzNSIsImlhdCI6MTY1MzQ1OTc5Nn0.rXzw6bUifWESmOfEEa4jgbiIaMyepXltIneJx9VCxrakmnRn6r1nScTpSxOJoytLDK48IKkhp6vB8Klfz-7wuecrb7jXPbZh1LzOe4d2ocn5JkJtIus_aZiz0pA5cdRb-6KrrTQCl",
    "expiresIn": 1800,
    "refreshToken": "eyJhbGciOiJSUzUxMiJ9.eyJzdWIiOiIzMS0xNzM3LTUyMzUtNzEzNSIsImNsaWVudElkIjoiaGVhbHRoaWQtYXBpIiwic3lzdGVtIjoiQUJIQS1OIiwidHlwIjoiUmVmcmVzaCIsImV4cCI6MTY1Mzg5MTc5NiwiaWF0IjoxNjUzNDU5Nzk2fQ.kd33V0NKtjJ5l8VZk7lscF6tLQR1m721VDcGyzkibyr3D0dtcJORODBvMLKcAJmwFM6KXyV51LHOpj-w9JkxE_eWY4L8YaZbQ2Rx36j",
    "refreshExpiresIn": 432000
}
```


\
\
\
## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Reactivate_ABHA_Via_Mobile_Otp.json)

**Download the Curls** [here](/abdm-docs/Curls/)



