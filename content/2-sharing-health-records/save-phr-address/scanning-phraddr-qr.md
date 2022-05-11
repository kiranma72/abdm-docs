---
title: "By scanning PHR Address QR"
date: 2022-05-07T18:00:04+05:30
weight: 2
draft: false
---

## Overview of the functionality 
- Patient must have a PHR app or PHR card and have a valid PHR address
- Hospital must have a scanner available at the registration counter
- Hospital operator scans the QR code on patient PHR card or from PHR mobile App.
- After scanned HIP will call the share-profile API on the HIE-CM 
- The HIE-CM will verify this is a registered healthcare provider and call the share-profile api on the end of the HRP that is linked to this HIP 
- The HRP software can create a screen to display all the scanned profiles and allow the operator to select them for fast registration 
- Then the detials like ABHA ID, PHR address,name,gender,sateId,districtId,dob,address will be shared with health facility


![Scan PHR QR Code](/abdm-docs/img/PHRAddress_QRCode.png)

## API Sequence 


## API Information Request Response 

1. Get patient's Details

**URL:** https://dev.abdm.gov.in/cm/v0.5/patients/profile/share

**Request:** POST  

**Parameters:**

- Authorization: Access token which was issued after successful login with gateway auth server.

Type: string (header)

- X-HIP-ID : Identifier of the health information provider to which the request was intended.

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


2. Response to patient's share profile request

**URL:** https://dev.abdm.gov.in/gateway/v0.5/patients/profile/on-share

**Request:** POST  

**Parameters:**

- Authorization: Access token which was issued after successful login with gateway auth server.

Type: string (header)

- X-CM-ID: Suffix of the consent manager to which the request was intended.

Type: string (header)

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-11T04:58:00.037Z",
  "acknowledgement": {
    "status": "SUCCESS",
    "healthId": "<username>@<suffix>"
  },
  "error": {
    "code": 1000,
    "message": "string"
  },
  "resp": {
    "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  }
}
```

**Response:**

202	

Request Accepted



## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/scanning-phraddr.json)

**Download the Curls** [here](/abdm-docs/Curls/scanning-phraddr.txt)

