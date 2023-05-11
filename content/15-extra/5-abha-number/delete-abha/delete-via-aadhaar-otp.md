---
title: "Delete ABHA via Aadhaar Otp"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---

# Delete ABHA via Aadhaar Otp

## Overview of the functionality 

- Users may delete his/her ABHA (Health ID) permanently.

Following will happen if you delete your ABHA (Health ID) :
1. Your ABHA (Health ID) will be permanently deleted, along with all your demographic details .
2. You will not be able to retrieve any information tagged to your ABHA (Health ID) in future.
3. You will never be able to access ABDM applications or any health records over the ABDM network with your deleted ABHA (Health ID).


## API Sequence 

The sequence of APIs used via this method is shown in the diagram below.

![Delete ABHA via Aadhaar Otp](/abdm-docs/img/Delete_ABHA(Health_ID).png)


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
**3. Generate Aadhaar OTP on Registered for link account with aadhar number**

Api Accepts Auth Token and Generates OTP on Linked mobile number.Generate Aadhaar OTP on mobile number linked with Aadhar

Explanation - API accepts Auth Token and Generates OTP on Linked mobile number.

Request Body - Required

Response - API accepts Auth Token and Generates OTP on Linked mobile number. Returns Error for Unauthorized token .

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/aadhaar/generateOTP

**Request:** POST  

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

- X-HIP-ID string (header) : your-HIP-ID

- X-Token string (header) : Bearer your-X-token


**Body:**

aadharNumberWebOptionalRequestPayload  (body)

```json
{

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
**4. Delete the account using aadhaar otp.**

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/profile/delete

**Request:** POST  

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

- X-HIP-ID string (header) : your-HIP-ID

- X-Token string (header) : Bearer your-X-token


**Body:**

deleteAccountByOtpWebRequest  (body)

```json
{
  "authMethod": "AADHAAR_OTP",
  "otp": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI=",
  "reasons": ["205"],
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 204




## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Delete_ABHA_Via_Aadhaar_Otp.json)

**Download the Curls** [here](/abdm-docs/Curls/)






