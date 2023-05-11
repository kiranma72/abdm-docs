---
title: "Update Email"
date: 2022-05-07T18:00:04+05:30
weight: 3
draft: false
---


## Update User E-mail


### Overview of the functionality 

- OTP will be sent to the provided e-mail address.
- OTP will be valid for 10 minute only.
- To Update or Changes the existing e-mail Address (Verified/Unverified email).
- Send the New Email Address required in the request.

## API Sequence 


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



**3. To generate the Email Verification OTP to verify the Email Address in the profile. OTP will be sent to the provided email address.**

**Note:**

- To verify the Email Address provided by the beneficiary during the registration process, OTP will be sent to the email address. Send the Email Address in the request.

- Email Verification OTP will be valid for 10 minutes only.

- To Update or Changes the existing e-mail Address (Verified/Unverified email). Send the New Email Address* required in the request.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/email/verification/send/otp

**Need to check this API not in sandbox swagger**

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

request (body)

```json
{
  "emailAddress": "user@xyz.com"
}
```

**Response:** 200  OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```



**4. Verify the Email Verification OTP to verify the E-mail Address.**

Transaction ID & encrypted OTP is passed in the requested body. An authentication token is used in the header. OTP should be in the encrypted form. Status is returned in 
the response body


**Notes:**

- Verification OTP received over the email address. OTP* required and transaction id* required should be passed in the request.

- OTP must be in the encrypted.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/email/verification/verify/otp

**Need to check this API not in sandbox swagger**

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

request (body)

```json
{
  "encryptedOtp": "m8kr0P9pDNgvB1g0CoSWEcDb+7AicoQijHcReUa3LbO8C8qDqSd2Lk19wua+LXGelahasnOy2L+oAsrLoZtHJF5qROnuultKjKphFPQWkRIY3RmJ2ygwjJzEhVL5ATFzzFVCTKjwG4DwRiL01r4OsOy/dgzAu+LHtNAkxxCKRV5trZOENhRoGzfGEFloVhIkfZkdgq4YmOWfIOOeBxU4U8OpxUWU0FSvK38RH45R5MLFh8x5vM6qBCfW3BRYu0Wg8pKnhGgRpbRURVCv4PvhEfHTBVGAJ6deGpD/8aKLTPGj9aHqr8sjiPiZKwN1PmRNO9CdT9T1HjfOEtxH1sBDARNSvnNm0HS/BS4FQ9cRQ4wNqfegpXO6mi2kqB9MjqZ+yDvciBAv/HZJ7qPUgnkFbKiCom1ay248JtNrzPgRhtjJ6DkY+ZtNtS3lHQO+pXUnueJjttcOm9n7sbSwFSE810si4M24Q1989yYCeJ3pGriHFkBaCLetCAMgKN4XIEf9/sIBH0VGJzaEXFCEVFhUeSOiCDOn8b0ePlCH1R702W7untdaGUia/vuD2SeCxmAJGx31WxLYiQolRkWIX4Yi6mZZ8v2JvvR+MtE6JPWh3KUVrKvLE+3nFsYrLhxHDXuQu69enHkd7PRGsr18pyWxUywxDB8W8QKltx0IS+nDvHI=",
  "txnId": "c3b0c27d-e19d-4244-b8bb-3fa19285054a"
}
```

**Response:** 200  OK

```json
{
  true
}
```




## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Update_Email.json)

**Download the Curls** [here](/abdm-docs/Curls/)
