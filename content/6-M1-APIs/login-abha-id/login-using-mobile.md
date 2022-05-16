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



**2. Generate Mobile OTP to start registration transaction**

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



**2. Verify Mobile OTP sent as part of registration transaction.**

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



3. Login to ABHA Number with verified mobile token

Explanation - API Checks Details and creates ABHA Number

Request Body - Required

Response - API Checks Details and creates ABHA Number

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
	
Return Account Details in case of success

Example Value
Model
{
  "authMethods": "AADHAAR_OTP",
  "dayOfBirth": "23",
  "districtCode": "401",
  "districtName": "Pune",
  "email": "Example@demo.com",
  "firstName": "akash",
  "gender": "M",
  "healthId": "deepak.pant",
  "healthIdNumber": "43-4221-5105-6749",
  "kycPhoto": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkJCQkJCQoLCwoODw0PDhQSERESFB4WFxYXFh4uHSEdHSEdLikxKCUoMSlJOTMzOUlUR0NHVGZbW2aBeoGoqOIBCQkJCQkJCgsLCg4PDQ8OFBIRERIUHhYXFhcWHi4dIR0dIR0uKTEoJSgxKUk5MzM5SVRHQ0dUZltbZoF6gaio4v/CABEIBLAHgAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwABBAUGB//aAAgBAQAAAADwawLpMspcK7qrlE5F0Vtul2bVywMUNeBHUkW/bmxvYELGuNjh2VDvixxo5ViljKjDRMoahCULjs2JCShjhjh2OGxo0Y2MoXHOLszsKLhw7tD99mpZQxj8xceofmLEKFwXLTIyHwY1Ls+iEotjHY0M0pjRYxtGj4VFKLPohQlFQyy4Qipc0XG9pS+CP/2Q==",
  "lastName": "singh",
  "middleName": "pramod",
  "mobile": "9545812125",
  "monthOfBirth": "05",
  "name": "kishan kumar singh",
  "new": true,
  "profilePhoto": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkJCQkJCQoLCwoODw0PDhQSERESFB4WFxYXFh4uHSEdHSEdLikxKCUoMSlJOTMzOUlUR0NHVGZbW2aBeoGoqOIBCQkJCQkJCgsLCg4PDQ8OFBIRERIUHhYXFhcWHi4dIR0dIR0uKTEoJSgxKUk5MzM5SVRHQ0dUZltbZoF6gaio4v/CABEIBLAHgAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwABBAUGB//aAAgBAQAAAADwawLpMspcK7qrlE5F0Vtul2bVywMUNeBHUkW/bmxvYELGuNjh2VDvixxo5ViljKjDRMoahCULjs2JCShjhjh2OGxo0Y2MoXHOLszsKLhw7tD99mpZQxj8xceofmLEKFwXLTIyHwY1Ls+iEotjHY0M0pjRYxtGj4VFKLPohQlFQyy4Qipc0XG9pS+CP/2Q==",
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "stateCode": "27",
  "stateName": "MAHARASHTRA",
  "tags": {
    "additionalProp1": "string",
    "additionalProp2": "string",
    "additionalProp3": "string"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "yearOfBirth": "1995"
}
```








## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)

