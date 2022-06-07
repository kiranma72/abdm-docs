---
title: "By sharing PHR Address verbally"
date: 2022-05-07T18:00:04+05:30
weight: 3
draft: false
---

## Overview of the functionality 
- Patient must have a valid PHR address
- Patient verbally shares the PHR address to the health facility during registration
- Facility initiates a mobile OTP authentication for this PHR address
- Then patient will receive an OTP on their mobile which they must share with the operator 
- The facility sends the OTP to the HIE-CM. On successful validations it gets the demographic details of the user and a new linking token 
- The HRP software must store this access(linking) token in their system for the purpose of linking care contexts to the patient.


![Sharing PHR Verbally](/abdm-docs/img/share_phr_verbally.PNG)


## API Sequence 


![Mobile Authentication Flow](../share-phraddr-verbally.png)


## API Request Response 

### 1. Get a patient's authentication modes

**URL:** https://dev.abdm.gov.in/gateway//v0.5/users/auth/fetch-modes
**HEADERS:**
- Authorization: JWT Sessions token 
- X-CM-ID: Should be the domain in the PHR Address - sbx or abdm
**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T08:51:12.728Z",
  "query": {
        "id": "kiranma@sbx",
        "purpose": "KYC_AND_LINK",
        "requester": {
            "type": "HIP",
            "id": "Demo_Test_001"
        }
    }
}
```

**Response:**
202	  Accepted


### 2. Accept callback with supported authentication modes for this PHR Address

**URL:** {HRP CALLBACK URL}/v0.5/users/auth/on-fetch-modes
**Request:** POST  
**HEADERS:**
- Authorization: GW JWT token 
- X-HIP-ID: Same HIP id that was passed in the auth init 
**Body:**

```json
{
  "requestId": "b4a4084b-b44d-4626-8134-dc5c7453c467",
  "timestamp": "2022-06-01T06:49:05.826893",
  "auth": {
    "purpose": "KYC_AND_LINK",
    "modes": [
      "MOBILE_OTP",
      "DEMOGRAPHICS"
    ]
  },
  "error": null,
  "resp": {
    "requestId": "ff85e8ce-3051-4984-8df2-058e9e986dc1"
  }
}
```

**Response:**
202	 Accepted

Example callback if the PHR address shared is uncorrect 
```json
{
  "requestId": "aba1b025-e371-495d-8698-f3f0b1395964",
  "timestamp": "2022-06-01T06:52:31.169551",
  "auth": null,
  "error": {
    "code": 1437,
    "message": "Account with ABHA number/Username not found."
  },
  "resp": {
    "requestId": "3d001a45-d1d2-469d-bb2b-2bb106a3f42c"
  }
}
```


### 3. Initialize authentication from HIP

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/init
**HEADERS:**
- Authorization: JWT Sessions token 
- X-CM-ID: Should be the domain in the PHR Address - sbx or abdm
**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T08:59:28.977Z",
  "query": {
    "id": "kiranma@sbx",
    "purpose": "KYC_AND_LINK",
    "authMode": "MOBILE_OTP",
    "requester": {
      "type": "HIP",
      "id": "Demo_Test_001"
    }
  }
}
```

**Response:**
202	  Accepted


### 4. Response to user authentication initialization 

**URL:** {HRP CALLBACK URL}/v0.5/users/auth/on-init
**Request:** POST  
**HEADERS:**
- Authorization: GW JWT token 
- X-HIP-ID: Same HIP id that was passed in the auth init 
**Body:**

```json
{
  "requestId": "eecfe297-9981-421b-82c6-af923243f7b9",
  "timestamp": "2022-06-01T06:59:09.121917",
  "auth": {
    "transactionId": "bc4f84e8-5c37-41a3-98cd-b4b1beb95530",
    "mode": "MOBILE_OTP",
    "meta": {
      "hint": null,
      "expiry": "2022-06-01T08:59:09.121925"
    }
  },
  "error": null,
  "resp": {
    "requestId": "03ebec17-ae2e-4630-8fcf-ec5b69f7920c"
  }
}
```

**Response:**
202	 Accepted

User will get a SMS on their mobile phone with a OTP from the HIE-CM. Collect this OTP from the user and send it via the next API

### 5. Confirmation request by sending token, otp 

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/confirm
**HEADERS:**
- Authorization: JWT Sessions token 
- X-CM-ID: Should be the domain in the PHR Address - sbx or abdm
**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T09:05:40.735Z",
  "transactionId": "bc4f84e8-5c37-41a3-98cd-b4b1beb95530",
    "credential": {
       "authCode":"704249"
  } 
  }
}
```
Ensure the transaction ID is the same as obtained in the on-init callback

**Response:**
202	  Accepted


### 6. Callback from HIE-CM with KYC and Token information
**URL:** {HRP CALLBACK URL}/v0.5/users/auth/on-confirm
**Request:** POST  
**HEADERS:**
- Authorization: GW JWT token 
- X-HIP-ID: Same HIP id that was passed in the auth init 
**Body:**
```json
{
  "requestId": "9f7eb8ad-a35a-4ffd-9700-8b608c387778",
  "timestamp": "2022-06-01T07:00:58.782868",
  "auth": {
    "accessToken": "eyJhbGciOiJSUzUxMiJ9.eyJzdWIiOiJraXJhbm1hQHNieCIsInJlcXVlc3RlclR5cGUiOiJISVAiLCJyZXF1ZXN0ZXJJZCI6IkRlbW9fVGVzdF8wMDIiLCJwYXRpZW50SWQiOiJraXJhbm1hQHNieCIsInNlc3Npb25JZCI6ImViZTcyNTU4LTI2N2EtNDVkNS1hMzk1LTZlMjAzNTI3YzhlYyIsImV4cCI6MTY1NDE1MzI1OCwiaWF0IjoxNjU0MDY2ODU4fQ.ZxWtxkOiW9C2xF3KAn0-w_L9oO9tYhCMGZ_CAhRNY47owCXwgvhc1QgHdawPWjwsMN0ARzrOaPAtHKUmj4q19E52jyuR_ONdej6qD1Mf-uaRkdOaqrF3ICLS2q2icqanvEznixJXTfaS15-9Yg8LL3AEwF7V6nxmZWbrPHfSizoUedfMPZEkLxcwJQCjfNLu7Igd_gv6GC4cscKOIEz0B2ilYuAWKRQ521VSTE-GZOPWSCA3O_oAFW_i8AOy84rvcpKEFOM9qmyFKksWKdFeK-HKQOA68IGDqbwUDXt4R5qNzXP2C1lk5eAwZlzKhYr8Vj3eyWMUrhYFLSTfoRjRuw",
    "patient": {
      "id": "kiranma@sbx",
      "name": "Kiran Anandampillai",
      "gender": "M",
      "yearOfBirth": 19xx,
      "monthOfBirth": 9,
      "dayOfBirth": XX,
      "address": {
        "line": null,
        "district": "CHANDIGARH",
        "state": "CHANDIGARH",
        "pincode": null
      },
      "identifiers": [
        {
          "type": "MOBILE",
          "value": "984X18X7XX"
        },
        {
          "type": "HEALTH_NUMBER",
          "value": "42-7175-8604-4553"
        }
      ]
    }
  },
  "error": null,
  "resp": {
    "requestId": "bda7b167-85b0-4bdf-b9e2-ae4bfd48326a"
  }
}
```
**Response:**
202	 Accepted


## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/shared-verbally.json)

**Download the Curls** [here](/abdm-docs/Curls/shared-verbally.txt)

