---
title: "By scanning HIP QR code"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---

## Overview of the functionality 
- Patient must have a PHR app and have a valid PHR address
- Hospital must generate a HIP QR code and display it at the registration counter
- Patient scans the QR code from his phone camera or his PHR app 
- If scanned from phone camera -- The list of installed PHR apps is shown on the phone. The user can select any of the apps 
- if scanned from within the PHR app, the app will call the share-profile API on the HIE-CM 
- The HIE-CM will verify this is a registered healthcare provider and call the share-profile api on the end of the HRP that is linked to this HIP 
- The HRP software can create a screen to display all the scanned profiles and allow the operator to select them for fast registration 


include any images from the PHR app / EMRSBX for this feature 



## API Sequence 

## API Information Request Response 

1. Get patient's Details

**URL:** https://dev.abdm.gov.in/cm/v0.5/patients/profile/share

**Request:** POST  

**Parameters:**
- Authorization: Access token which was issued after successful login with gateway auth server.

Type: string (header)

- X-CM-ID: Suffix of the consent manager to which the request was intended.

Type: string (header)

**Body:**
```json
{
  "requestId": "499a5a4a-7dda-4f20-9b67-e24589627061",
  "timestamp": "2022-05-10T14:19:12.993Z",
  "profile": {
    "hipCode": "12345 (CounterId)",
    "patient": {
      "healthId": "<username>@<suffix>",
      "healthIdNumber": "1111-1111-1111-11",
      "name": "Jane Doe",
      "gender": "M",
      "address": {
        "line": "string",
        "district": "string",
        "state": "string",
        "pincode": "string"
      },
      "yearOfBirth": 2000,
      "dayOfBirth": 0,
      "monthOfBirth": 0,
      "identifiers": [
        {
          "type": "MR",
          "value": "+919800083232"
        }
      ]
    }
  }
}
```

**Response:**
202	
Request Accepted


## Postman + Curl Collection 

