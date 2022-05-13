---
title: "By sharing PHR verbally"
date: 2022-05-07T18:00:04+05:30
weight: 3
draft: false
---

## Overview of the functionality 
- Patient must have a valid PHR address
- Patient verbally shares the PHR address at the Health operator.
- OTP authentication will be required only if PHR address is shared verbally.
- 


include any images from the PHR app / EMRSBX for this feature 

## API Sequence 


| S.No | Collection & verification of ABHA by HIP	| APIs call on the Gateway|APIs that are expected to be available at the HIP end by the Gateway |
|------|------------------------------------------|-------------------------|---------------------------------------------------------------------|
|  1.  |Get patient's authentication modes relevant to specified purpose|https://dev.abdm.gov.in/gateway/v0.5/users/auth/fetch-modes |{{HIP_HOST}}/v0.5/users/auth/on-fetch-modes|
|  2.  |Demographic auth mode to be used for QR code scans|https://dev.abdm.gov.in/gateway/v0.5/users/auth/init |{{HIP_HOST}}/v0.5/users/auth/on-init|
|  3.  |Confirm authentication of users. Obtain linking token|https://dev.abdm.gov.in/gateway/v0.5/users/auth/confirm  |{{HIP_HOST}}/v0.5/users/auth/on-confirm|
|  4.  |Notification API in case of DIRECT mode of authentication|https://dev.abdm.gov.in/gateway/v0.5/users/auth/notify |{{HIP_HOST}}/v0.5/users/auth/on-notify |


## API Request Response 

1. Get a patient's authentication modes relevant to specified purpose

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/fetch-modes

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-HIP-ID  string (header)

**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T08:51:12.728Z",
  "query": {
    "id": "hinapatel79@ndhm",
    "purpose": "LINK",
    "requester": {
      "type": "HIP",
      "id": "100005"
    }
  }
}
```

**Response:**

202	  Accepted


2. Identification result for a consent-manager user-id

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/on-fetch-modes

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-HIP-ID  string (header)

- X-HIU-ID  string (header)

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T08:53:22.488Z",
  "auth": {
    "purpose": "KYC_AND_LINK",
    "modes": [
      "MOBILE_OTP"
    ]
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

202	 Accepted




3. Initialize authentication from HIP

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/init

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-CM-ID  string (header)

**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T08:59:28.977Z",
  "query": {
    "id": "hinapatel@ndhm",
    "purpose": "LINK",
    "authMode": "MOBILE_OTP",
    "requester": {
      "type": "HIP",
      "id": 100005
    }
  }
}
```

**Response:**

202	  Accepted


4. Response to user authentication initialization from HIP

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/on-init

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-HIP-ID  string (header)

- X-HIU-ID  string (header)

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T09:02:38.686Z",
  "auth": {
    "transactionId": "string",
    "mode": "MOBILE_OTP",
    "meta": {
      "hint": "string",
      "expiry": "2019-12-30T12:01:55Z"
    }
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

202	 Accepted




5. Confirmation request sending token, otp or other authentication details from HIP/HIU for confirmation

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/confirm

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-CM-ID  string (header)

**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T09:05:40.735Z",
  "transactionId": "string",
  "credential": {
    "authCode": "string",
    "demographic": {
      "name": "janki das",
      "gender": "M",
      "dateOfBirth": "1972-02-29",
      "identifier": {
        "type": "MOBILE",
        "value": "+919800083232"
      }
    }
  }
}
```

**Response:**

202	  Accepted


6. callback API for /auth/confirm (in case of MEDIATED auth) to confirm user authentication or not

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/on-confirm

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-HIP-ID  string (header)

- X-HIU-ID  string (header)

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T09:06:58.238Z",
  "auth": {
    "accessToken": "string",
    "validity": {
      "purpose": "LINK",
      "requester": {
        "type": "HIP",
        "id": 100005
      },
      "expiry": "2022-05-13T09:06:58.238Z",
      "limit": "1"
    },
    "patient": {
      "id": "<patient-id>@<consent-manager-id>",
      "name": "Hina Patel",
      "gender": "M",
      "yearOfBirth": 2000,
      "address": {
        "line": "string",
        "district": "string",
        "state": "string",
        "pincode": "string"
      },
      "identifiers": [
        {
          "type": "MR",
          "value": "+919800083232"
        }
      ]
    }
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

202	 Accepted


## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/shared-verbally.json)

**Download the Curls** [here](/abdm-docs/Curls/shared-verbally.txt)

