---
title: "Retrieve ABHA via Aadhaar OTP"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---


## Retrieve ABHA Number via Aadhaar OTP

## Overview of the functionality 

- To retrieve ABHA (Health ID), an OTP is sent on a registered mobile number and the user's health ID is retrieved from the ABDM server.
- The sequence of APIs used via this method is shown in the diagram below. 

## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![Login ABHA via Aadhaar Otp](/abdm-docs/img/Forgot_ABHA(Health_ID)_Retrieve_via_Aadhaar_OTP.png)


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




**3. Generate Aadhaar OTP on Registered mobile number**

Explanation - API accepts Aadhaar Number and then generates OTP for linked number as part of Forgot flow.

Request Body - Required

Response - Api Accepts Aadhaar Number and then generates OTP for linked number as part of Forgot flow. Returns Transaction ID.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/forgot/healthId/aadhaar/generateOtp

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

generateOtpRequest  (body)

```json
{
  "aadhaar": "iKLrJ3feg17bxK1+1Rlew8XjJxMiU5yLE+cndrlHU2gnCmKMiRG71B+VWUOMRLjDSHRuDVc7ZS2rSfN89/t2RkEq3JgX6saWgXLhy+ksz5Dw1xq0Tk9Ph6SeRV00Oz0AWPUk+/HETOtIlEYtgH8p3dvvW4WEZgWfIxBLCZ9CAqKKwoeZ+8xKnYaA2MRtcuVO5xZ20mJxirjohRtSlyT+TuB49Ena+UiscDijVSgh8Ghx5kgned/HcMoGZqC8bjajgw9QgphkD9tm0EOandrocF7oR5OfyM175csLrToVflTViuq/8vLFy++mBEx4LAI6BuN8PeVfKf4aM7V/f8gikwDQsY6RpGPG4BFKuqCbp5bGvUxTMPM2w09PaTB53+E6IWmy0ZSs9E6X3TcSdQHURJJfQ114lErGwDMyXEUCONnxDDjczyoD3KPJW/IyFpv38r0D4WzRQVhVYYtBecG3jlL4V3tszROIOz+cbmcjvXFP8UQ50G/ywGoIFaNwZSUGDaQ110s0Oul1PMWbfsfvL4n0WStK1nU1jhtPTtJJGojX3ZjtC2sWK63lj7HJZ/Pbl8KvcKso8dbuUjSRFiNu7nvHshit+zMn8HtSgLP48SyM5qW84gLhcvCQYvNKY9n3oUNibFycaENAs1j8sZxwkBPyDhnjpjCXHsqxdVmBfYo="
}
```

**Response:** 200 OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```



**4. Verify aadhar OTP sent as part of forget ABHA Number**

Explanation - API accepts OTP and then checks is it Valid as per given Aadhaar Transaction.

Request Body - Required

Responce - Api Accepts OTP then returns ABHA Number and ABHA Address accordingly.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/forgot/healthId/aadhaar

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

authAccountAadhaarOTPRequest  (body)

```json
{
  "otp": "OTQSOHslRqwlWfgYDcAVEAcbNLhV+fijVE1S5jmJWnI1csyyVJ5gLa116zd6MwkzBSehjuyhu7f+P0vlzkRJhLUsb3uneztaO2ZTzSSZRwNI3Rfv1GDOHIzQhat42TBNN3LBvspmfDcKnPS1zso9MoOH8CVxHp6on4QaMAABY4FazAPUhffRCpgo9/rwgaS/1hPJFwvDYcvhWbgYVKihx94yvZa9Iof1OPti0Lrk6NzIs0+BkWoeSssSrI8/sMZjsLmlq967vdbiUUQdTSinBdoWSe25SucaQ9YH4qCy1/ZiQEhPSVY/cJqLSwXufpOxjAm0dg0RuQ5ZakDj4SvkY4RZRWvoFeP6XBPyKWhPjBqvKLUWQt/lYyctynQFBIIBgNkuuXWfvgcMztbEDoJOpnRZ5foVKppVtyqn5tP90Ivuu7pgkVLOUvAHDhPWuIWDguXMu9iTRFm10msUuorMmSQjSpKBVvh005Z6vQmdfeFPi94HdzpIbGJRtTGytuQSipQjjFKxwF2D00//mOFDftdGUoa25rLlmldxjDo+diZm8xnRpn92MojFV759+vVprRaJLVtZpcaa5eCy8IWhSBPrub5VFv2heKq6WqkYXzybIbJBh+VCZSYBhZyc2hppGIsVWrUKnMbuscYjXLDFtE05s+BhZqIn4RwBQ++Fc1Y=",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200

```json
{
    "healthId": "test@sbx",
    "healthIdNumber": "12-3456-7890-1234",
    "jwtResponse": {
        "token": "string",
        "expiresIn": 1800,
        "refreshToken": "string",
        "refreshExpiresIn": 432000
    }
}
```




## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Retrieve_ABHA_Via_Aadhaar_Otp.json)

**Download the Curls** [here](/abdm-docs/Curls/)



