---
title: "Login to your ABHA using Mobile"
date: 2022-05-07T18:00:04+05:30
weight: 3
draft: false
---

## Login to your ABHA using Mobile

## Overview of the functionality 

- Users will now be able to login to their ABHA using their Mobile Number. 
- In case multiple ABHA numbers are linked to a Mobile Number, users will be able to choose the account they want to login to. 
- The patient must provide the OTP to the user to complete the authentication.
- To begin the process, the Authentication token public certificate API (V1.Auth/cert) is called.
- After that An OTP is sent to the patient’s mobile number that is linked with the ABHA.
- The patient must share the OTP with the user for verification.
- A token has been returned and can be used for Profile APIs purpose.


## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![Login ABHA ID via Aadhaar Otp](/abdm-docs/img/Login_With_ABHA_using_mobile.png)


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




**3. Generate Mobile OTP to start registration transaction**

Explanation - API accepts Mobile Number and then Generates OTP for it.

Request Body - Required

Response - API accepts Mobile Number and then Generates OTP for it. if number not found then throws error.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/registration/mobile/login/generateOtp

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

**Response:** 200 OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```



**4. Verify Mobile OTP sent as part of registration transaction.**

Explanation - API accepts OTP and then Checks OTP is Verified or Not

Request Body - Required

Response - API Accepts OTP and then Checks OTP is Verified or Not. if it is not verified then it shows Error.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/registration/mobile/login/verifyOtp

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

verifyMobileWebRequest  (body)

```json
{
  "otp": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI=",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200 OK

```json
{
  "txnid": "25c1b379-984c-4b56-a86f-58c386879149",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "mobileLinkedHid": {
    "healthIdNumber": "25-8180-3683-5375",
    "healthId": "string",
    "name": "priya",
    "profilePhoto": "string",
    "phrAddress": "string"
  }
}
```



**5. Login to ABHA Number with verified mobile token**

Explanation - API Checks Details and login ABHA Number

Request Body - Required

Response - API Checks Details and login ABHA Number

**URL:** https://healthidsbx.abdm.gov.in/api/v2/registration/mobile/login/userAuthorizedToken

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- T-Token string (header)


**Body:**

mobileLoginWebRequest  (body)

```json
{
  "healthId": "25-7840-4131-2620",
  "txnId": "25c1b379-984c-4b56-a86f-58c386879149"
}
```

**Response:** 200 OK

```json
{
    "token": "eyJhbGciOiJSUzUxMiJ9.eyJzdWIiOiIzMS0xNzM3LTUyMzUtNzEzNSIsImNsaWVudElkIjoiaGVhbHRoaWQtYXBpIiwic3lzdGVtIjoiQUJIQS1OIiwibW9iaWxlIjoiNzc5OTE1NDk5OCIsImhlYWx0aElkIjoidGVzdC4xMjM0NTY3QHNieCIsImV4cCI6MTY1Mjc2Mzk2MCwiaGVhbHRoSWROdW1iZXIiOiIzMS0xNzM3LTUyMzUtNzEzNSIsImlhdCI6MTY1Mjc2MjE2MH0.odBGQghgBkp3DeEhsmhl6YfZB37J0bWQ1Zgc1j9zZrEkQkrcjlrzA4p2OFEjOp9fE_3QkCzfHsLon5CrRLdt-TAbgej43HtTjE7ghmg6_kOLueeKK0wkOaVVUFHaI77WR0-WJMp49PAqdpGADyuTmlOBDA4OYUbWqBE9bTvssn3zlNl4DKG51EluFbDC1J84vHrMxr6QIsgAOm4jwlru_aAYB79dgh-_C04-YQbCJOOTzMm0yx8rFq0BQsk1JR6nvqdl3m4Pp7lMPYEkyTrbJi9QiRHpik1XrxYFgDYR-3l4xpWGgDdjEGSUFvpY05AoHeWb8_gFapxmbTS-lyBbb866TtkudX2JX8p_H3r4X3MgTl5yedYrX_IGzRpbipR6r6VHY-MmF7t_jmtRb--V5HtoNVEnAoHrLA1c5YGckLevl3Vp9RL8I3E46jRyTahyBjtZ_z00ECl3SeDjg15PeOUViXG3pReGbkd29F63rOxmmEZ6ETGL258BvEOICoF5EyQKNA8mnfELR3FGKwxeS8pbiCU8pHJsN9EIJ2MCyt-Ho56dlJhPipDY24OeAdkmk13G5FX-v-pw_6gIagSYM0kehONpbZgULNJnmT44_CUvL7jkGvtUvL2jZ-P4BXzZP0VSJ_qTeWNTSW_f-2_2Z7gB5j4JfNvBiLLu31l8abc"
}
```




## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Login_ABHA_Using_Mobile.json)

**Download the Curls** [here](/abdm-docs/Curls/)

