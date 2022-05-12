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


Api gets the user account information.

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/account/profile

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

**Response:** 200 OK

```json
{
  "address": "string",
  "authMethods": [
    "AADHAAR_OTP"
  ],
  "dayOfBirth": "string",
  "districtCode": "string",
  "districtName": "string",
  "email": "string",
  "firstName": "string",
  "gender": "string",
  "healthId": "string",
  "healthIdNumber": "string",
  "kycPhoto": "string",
  "lastName": "string",
  "middleName": "string",
  "mobile": "string",
  "monthOfBirth": "string",
  "name": "string",
  "new": true,
  "pincode": "string",
  "profilePhoto": "string",
  "stateCode": "string",
  "stateName": "string",
  "subDistrictCode": "string",
  "subdistrictName": "string",
  "tags": {
    "additionalProp1": "string",
    "additionalProp2": "string",
    "additionalProp3": "string"
  },
  "townCode": "string",
  "townName": "string",
  "villageCode": "string",
  "villageName": "string",
  "wardCode": "string",
  "wardName": "string",
  "yearOfBirth": "string"
}
```

## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)
