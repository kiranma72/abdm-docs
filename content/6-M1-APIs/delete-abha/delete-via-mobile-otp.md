---
title: "Delete ABHA via Mobile Otp"
date: 2022-05-07T18:00:04+05:30
weight: 2
draft: false
---

# Delete ABHA via Mobile Otp

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


\
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
    "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJBbFJiNVdDbThUbTlFSl9JZk85ejA2ajlvQ3Y1MXBLS0ZrbkdiX1RCdkswIn0.eyJleHAiOjE2NTMzNjkyNTYsImlhdCI6MTY1MzM2ODY1NiwianRpIjoiZDg5YTFlYmUtZWRlNS00Y2U4LWEwZTAtMTUzNGNjNzkyYjk0IiwiaXNzIjoiaHR0cHM6Ly9kZXYubmRobS5nb3YuaW4vYXV0aC9yZWFsbXMvY2VudHJhbC1yZWdpc3RyeSIsImF1ZCI6WyJyZWFsbS1tYW5hZ2VtZW50IiwiYWNjb3VudCJdLCJzdWIiOiIwNmJkNGZlNy04NjEyLTRiZmEtYTI1NS1iMDdiZmFjZmU1M2QiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJoZWFsdGhpZC1hcGkiLCJzZXNzaW9uX3N0YXRlIjoiNjU2NGY2N2UtZjM4My00NGRiLWIyOTY",
    "expiresIn": 600,
    "refreshExpiresIn": 1800,
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICIyMWU5NzA4OS00ZTcxLTQyNGEtOTAzYS1jOTAyMWM1NmFlNWYifQ.eyJleHAiOjE2NTMzNzA0NTYsImlhdCI6MTY1MzM2ODY1NiwianRpIjoiNGY1ZjZjMWYtYTk0Yy00ZjJmLThmZjctYTY2MDRiN",
    "tokenType": "bearer"
}
```


\
\
**2. Authentication token public certificate. This certificate is also used to encrypt the data.**

**URL:** https://healthidsbx.abdm.gov.in/api/v1/auth/cert

**Request:** GET  

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

- X-HIP-ID string (header) : your-HIP-ID

**Response:** 200   OK

string

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
**4. Delete the account using Mobile otp.**

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/profile/delete

**Request:**  POST  

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

- X-HIP-ID string (header) : your-HIP-ID

- X-Token string (header) : Bearer your-X-token


**Body:**

deleteAccountByOtpWebRequest  (body)

```json
	{
	  "authMethod": "MOBILE_OTP",
	  "otp": "hzrxZvR1zkG3GxlGIy6ECQwd7rzsQmsGtzeGqAmEXpnl9jnLJR4wAIoPmAUUJLyPRzseloH59cQStn3dW6hmSDfnfYS0DpYRfIubOIo3DjkiAFkBgJrGTt0EEvoGV7Y0PYtGaaHqyo3lPDzGEqqml2rwf5p3VA7jY5Ez87UFLYPmZ14haSqZxO7EFOZGLcs29yuy3X4XvjAnJmbh5kh81ctCufqMqzk3I3fRxTzR/n42g27ou2fvuCpn/K/wBGsezmhUGUYK0nnkyh7z/9Vw91vpiqQrZdYBEX8YxnESU4KlbkYLDMBIr41I0rka70CqRFNlOJR+M+zqhJsOflRl62rQc1Bghoh9jgzW4NAWTxCGPfS375q1dxMpc6hm4mtF1mCazlQwq8feyEw8UHp9Z/kTFhkffcEFbeVSunWztY3IctL5Mfz14KFXUJfcBqt9EOTzjM15YUc/x6fBQ9P8Ix4/tP4kEUDeqyI6KVghZZsfLNaa+rvl/J4qiAA3SiXqA0adF1Hn9I2So8pFC/IvyRsFtQXo90JqwHVQYLA7Q1dIWSlPjAmObL3d65Zbb8xPg1xYLDoUUfk5kpU6hAhLom80N3d14eSvY+yzNsc1q09Wh9hgaDhUvs0CwBY0Xi0aYbhcZu26Wv3tNE4SOx5SsmqwSFwU41W281M3mHIfw5o=",
	  "reasons": ["205"],
	  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
	}
```

**Response:**  204




## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Delete_ABHA_Via_Mobile_Otp.json)

**Download the Curls** [here](/abdm-docs/Curls/)




