---
title: "Get User profile"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---


## Get User profile

## Overview of the functionality 

- Get the User profile

## API Sequence 


## API Information Request Response 


Get account information.

Explanation - Api Accepts Auth Token and then Returns Account Details.

Request Body - Required

Responce - Api Accepts Auth Token and then Returns Account Details. Returns Error for Unauthorized Auth Token.

**URL:** https://healthidsbx.abdm.gov.in/api/v1/account/profile

**Request:** GET  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

```json
{
  
}
```

**Response:** 200

```json
{
  "address": "b-14 someshwar nagar",
  "authMethods": "AADHAAR_OTP",
  "dayOfBirth": "31",
  "districtCode": "401",
  "districtName": "Pune",
  "email": "example@demo.com",
  "emailVerified": true,
  "firstName": "kishan",
  "gender": "Male",
  "healthId": "deepakndhm",
  "healthIdNumber": "43-4221-5105-6749",
  "kycPhoto": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI=",
  "kycVerified": true,
  "lastName": "singh",
  "middleName": "kumar",
  "mobile": "9545812125",
  "monthOfBirth": "05",
  "name": "kishan kumar singh",
  "new": true,
  "phrAddress": [
    "string"
  ],
  "pincode": "412306",
  "profilePhoto": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkJCQkJCQoLCwoODw0PDhQSERESFB4WFxYXFh4uHSEdHSEdLikxKCUoMSlJOTMzOUlUR0NHVGZbW2aBeoGoqOIBCQkJCQkJCgsLCg4PDQ8OFBIRERIUHhYXFhcWHi4dIR0dIR0uKTEoJSgxKUk5MzM5SVRHQ0dUZltbZoF6gaio4v/CABEIBLAHgAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwABBAUGB//aAAgBAQAAAADwawLpMspcK7qrlE5F0Vtul2bVywMUNeBHUkW/bmxvYELGuNjh2VDvixxo5ViljKjDRMoahCULjs2JCShjhjh2OGxo0Y2MoXHOLszsKLhw7tD99mpZQxj8xceofmLEKFwXLTIyHwY1Ls+iEotjHY0M0pjRYxtGj4VFKLPohQlFQyy4Qipc0XG9pS+CP/2Q==",
  "stateCode": "27",
  "stateName": "MAHARASHTRA",
  "subDistrictCode": "213",
  "subdistrictName": "Baramati",
  "tags": {
    "additionalProp1": "string",
    "additionalProp2": "string",
    "additionalProp3": "string"
  },
  "townCode": "27",
  "townName": "Baramati",
  "verificationStatus": "verified",
  "verificationType": "testing",
  "villageCode": "412",
  "villageName": "Someshwar Nagar",
  "wardCode": "08",
  "wardName": "Sinhgad fort ward",
  "yearOfBirth": "1994"
}
```

## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)
