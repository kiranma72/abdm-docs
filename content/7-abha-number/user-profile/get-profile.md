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



**Response:** 200  OK


```json
{
    "healthIdNumber": "12-3456-7890-1234",
    "healthId": "12345678901234@sbx",
    "mobile": "1234567890",
    "firstName": "ABHI",
    "middleName": "RAM",
    "lastName": "A",
    "name": "ABHI RAM A",
    "yearOfBirth": "1977",
    "dayOfBirth": "1",
    "monthOfBirth": "1",
    "gender": "M",
    "email": "ram@demo.com",
    "profilePhoto": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2",
    "stateCode": "34",
    "districtCode": "",
    "subDistrictCode": null,
    "villageCode": null,
    "townCode": null,
    "wardCode": null,
    "pincode": "123456",
    "address": "delhi",
    "kycPhoto": null,
    "stateName": "delhi",
    "districtName": "delhi",
    "subdistrictName": null,
    "villageName": null,
    "townName": "delhi",
    "wardName": null,
    "authMethods": [
        "AADHAAR_BIO",
        "AADHAAR_OTP",
        "DEMOGRAPHICS",
        "PASSWORD",
        "MOBILE_OTP"
    ],
    "tags": {},
    "kycVerified": true,
    "verificationStatus": null,
    "verificationType": null,
    "phrAddress": [
        "12345678901234@sbx"
    ],
    "emailVerified": false,
    "new": false
}
```



## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Get_User_Profile.json)

**Download the Curls** [here](/abdm-docs/Curls/)
