---
title: "Update Mobile via Aadhaar Otp"
date: 2022-05-07T18:00:04+05:30
weight: 4
draft: false
---

## Update Mobile via Aadhaar Otp

## Overview of the functionality 

- To update the mobile using Aadhaar OTP , a client ( Integrator) needs to first generate Mobile OTP and verify it.
- Again generate Aadhaar OTP and a transaction ID is returned.
- Auth token, OTP, old password along with transaction ID is passed in the requested body and client is returned with the status of changed mobile number.

## API Sequence 

The sequence of APIs used via this method is shown in the diagram below.

![Update Mobile via Aadhaar Otp](/abdm-docs/img/)

**Need to confirm API flow snapshot provided in pdf is not correct**

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




**3. Generate OTP on new mobile need to update existing account mobile number**

Explanation - Api Accepts New Mobile Number and Auth Token and creates OTP.

Request Body - Required

Responce - Api Accepts New Mobile Number and Auth Token and creates OTP. Returns Error for Unauthorized Auth Token.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/change/mobile/new/generateOTP

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

mobileNumberNewRequestPayload (body)

```json
{
  "newMobileNumber": "9545812125"
}
```

**Response:** 200  OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```



**4. Verify Mobile OTP to complete new mobile update verification.**

Explanation - Api Accepts New Mobile Number OTP and Verifies it.

Request Body - Required

Responce - Api Accepts New Mobile Number OTP and Verifies it. Returns Error for Unauthorized OTP.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/change/mobile/new/verifyOTP

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

VerifyMobileWebRequest (body)

```json
{
  "otp": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI=",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200  OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```




**5. Generate Aadhaar OTP on Registered mobile number to start mobile update.**

Explanation - Api Accepts Transaction ID and Creates OTP for linked mobile number.

Request Body - Required

Responce - Api Accepts Transaction ID and Creates OTP for linked mobile number. Returns Error for Unauthorized Transaction ID.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/change/mobile/aadhaar/generateOTP

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

updateMobileGenerateOTPPayload (body)

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200  OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```




**6. Change mobile number via password/aadhaar/existing mobile for Health ID.**

Explanation - Api Accepts password/aadhaar/existing mobile and new Mobiles OTP and Updates new mobile number.

Request Body - Required

Responce - Api Accepts password/aadhaar/existing mobile and new Mobiles OTP and Updates new mobile number. Returns Error for Unauthorized OTP.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/change/mobile/update/authentication

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

updateNewMobileNoRequestPayload (body)

```json
{
  "authMethod": "AADHAAR_OTP",
  "oldPassword": "UPjUGDnhCi7aaoVLMpR99wtpDKm58vjdFx1ref++/v2u+CN+/P4AKwQQgMNoMs1MPv8cosEebxBMMQN8qdy9Y1WWz8Fp4U3gXxGEAOl848uRItXNm9peyOm8gZewmH4FtEAvA6tGVts3FG8fFBct0RCYLQAnlTQrO7hbjz81LYcI6aOw3tcZVXfdoQJjC5mGhnXQmloVciduw478IVUkx4VA/A5Y8jLuEqLsujYbx46MB1ZKWPTvTfopMU5VxLdWNrvSubSBrFeHNQRDS8jB35AC1zEZbnbPPU5fuLvFlsYXedq9XvQZK/S4qzdjkgHVUFeGN/9zvpsoC/0AifJ19tsPCKik1GeXdL+iDqpPIIS65kAAKQ7W8loMSBcXDy7/YU0S9VbiwM4xNGV3Fp/lQHY/0p3p0lGykmifr1V5IrFNo1vTZqXTAvysf4F9d7lIGVj6+TNYojg4NnO7iRO6UhZtNEjhDEED55qH8z4Qzv8R8ZpOOMIR3HLlWadnVKFeLsko9QwLcabV7caY25sTXzLK3dOXnH/AHqneWkksiCcz/GBrVgNG6D82XxgqQT8IzIyHQl0on1rIPJU6VAZ/i++JyP9xEjSI8TjJuGS6eH2KO19mIFjyqvhFLe0vFyeLTLFWphv3KPNTneMPCixlGf0ksjaCwQGChHobC4eqWyY=",
  "otp": "UPjUGDnhCi7aaoVLMpR99wtpDKm58vjdFx1ref++/v2u+CN+/P4AKwQQgMNoMs1MPv8cosEebxBMMQN8qdy9Y1WWz8Fp4U3gXxGEAOl848uRItXNm9peyOm8gZewmH4FtEAvA6tGVts3FG8fFBct0RCYLQAnlTQrO7hbjz81LYcI6aOw3tcZVXfdoQJjC5mGhnXQmloVciduw478IVUkx4VA/A5Y8jLuEqLsujYbx46MB1ZKWPTvTfopMU5VxLdWNrvSubSBrFeHNQRDS8jB35AC1zEZbnbPPU5fuLvFlsYXedq9XvQZK/S4qzdjkgHVUFeGN/9zvpsoC/0AifJ19tsPCKik1GeXdL+iDqpPIIS65kAAKQ7W8loMSBcXDy7/YU0S9VbiwM4xNGV3Fp/lQHY/0p3p0lGykmifr1V5IrFNo1vTZqXTAvysf4F9d7lIGVj6+TNYojg4NnO7iRO6UhZtNEjhDEED55qH8z4Qzv8R8ZpOOMIR3HLlWadnVKFeLsko9QwLcabV7caY25sTXzLK3dOXnH/AHqneWkksiCcz/GBrVgNG6D82XxgqQT8IzIyHQl0on1rIPJU6VAZ/i++JyP9xEjSI8TjJuGS6eH2KO19mIFjyqvhFLe0vFyeLTLFWphv3KPNTneMPCixlGf0ksjaCwQGChHobC4eqWyY=",
  "txnId": "c3b0c27d-e19d-4244-b8bb-3fa19285054a"
}
```

**Response:** 200  OK

string



## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Update_Mobile_Via_Aadhaar_Otp.json)

**Download the Curls** [here](/abdm-docs/Curls/)
