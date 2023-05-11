---
title: "Reactivate ABHA via Aadhaar OTP"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---



# Reactivate ABHA via Aadhaar OTP

## Overview of the functionality 

- Users may Reactivate his/her ABHA (Health ID) via Aadhaar OTP by using the below endpoints.

## API Sequence 


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
    "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJBbFJiNVdDbThUbTlFSl9JZk85ejA2ajlvQ3Y1MXBLS0ZrbkdiX1RCdkswIn0.eyJleHAiOjE2NTMzNjkyNTYsImlhdCI6MTY1MzM2ODY1NiwianRpIjoiZDg5YTFlYmUtZWRlNS00Y2U4LWEwZTAtMTUzNGNjNzkyYjk0IiwiaXNz",
    "expiresIn": 600,
    "refreshExpiresIn": 1800,
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICIyMWU5NzA4OS00ZTcxLTQyNGEtOTAzYS1jOTAyMWM1NmFlNWYifQ.eyJleHAiOjE2NTMzNzA0NTYsImlhdCI6MTY1MzM2ODY1NiwianRpIjoiNGY1ZjZjMWYtYTk0Yy00ZjJmLThmZjctYTY2MDRiN2M2ZjJhIiwiaXNz",
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
**3. Initiate authentication for reactivation of ABHA (Health ID)**

**URL:** https://healthidsbx.abdm.gov.in/api/v2/auth/reactivate/init

**Request:** POST  

**Parameters:**

- Authorization : Access token which was issued after successful login with gateway auth server

string (header)

- X-HIP-ID : Identifier of the health information provider to which the request was intended

string (header)


**Body:**

authRequest  (body)

```json
{
  "authMethod": "AADHAAR_OTP",
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
**4. Confirm reactivation txn with aadhar otp**

**URL:** https://healthidsbx.abdm.gov.in/api/v2/auth/reactivate

**Request:** POST  

**Parameters:**

- Authorization : Access token which was issued after successful login with gateway auth server

string (header)

- X-HIP-ID : Identifier of the health information provider to which the request was intended

string (header)


**Body:**

reactivateByOTPWebRequest  (body)

```json
{
  "authMethod": "AADHAAR_OTP",
  "otp": "P/6Z0hpCoXsHLUGLvzFrYG7o3LaRJB7jRN+Sdb8yuO7HOHpi0f2JhqdB/frJUJ84DDNa6DBClzPKsNbzOoRRAAGHktpD69WN2WFzfQDyAAwCpH2O4Q9MbzEIkh54NvJhhIguIt/7nLpV25DT+YRshwm3KNDixH7fUsIbaKRevzT3PzFzi8vpvgVCzjVPauGMf9Rgnk7e72hB4uPv1C1wbVImD/9ldfm4u/hbJKbH67QFdcWB4ctCPCflKm8BWNwkJlY6oUQsonktkAsesQMDLDcl1Bmw1Eu/vL2e5mOENL97Mase+uxKTmCzsiQwNyLZmqNL614oPOGp1yl631BDcjBjOR1mUUiNmABDww/3CnmmxbBopmuoDiSypSjLEcQW86s6TSMHuY9jsgB+Sz+C+T17Zid6pS5ALC+CQD2Vz/RNmvE6b0D0OBz//Nd9fVYesv/PLCd19YFr5J7UMMwWRaFPF8pBGR0GJXlY4HOvAPHHZw5ULVr7QYztQFMZzhaTOQtKeMkUh+/X8RdBxYruTB3dmmmjz6UXZHJoGC7TvfNzImC9+LvTzdreq8XhEL74LG1Gzyroi+x5lu6bFEQT1t1fb4vInwyQChFmxgPExA4NgfEytORdnPilZvppdwMUhLDFTUs9re4VMgotzD0MbQCIJ+ZLCV7EGic9vZVO54A=",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200   OK

```json
{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "expiresIn": 1800,
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "refreshExpiresIn": 432000
}
```




## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Reactivate_ABHA_Via_Aadhaar_Otp.json)

**Download the Curls** [here](/abdm-docs/Curls/)



