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


![Scan HIP QR Code](/abdm-docs/img/Scan HIP QR.png)

######## Patients can scan a Health Facility QR code Pasted at the facility registration counter on their PHR mobile app


**To use this flow for an HIP, follow the below steps**

- Generate a QR code for the data in below format. For testing we can use something like [Sample QR Generator](https://www.the-qrcode-generator.com/)

```json
{
    "hipId": "<HIP ID>",
    "code": "<any extra information you want to send in profile, e,g counterId, Dept Id>"
}
```

- Go to ABHA Mobile Application, then My Profile and Find Scan option on the top right.
- Scan the QR code, the app should fetch details of QR code along with User profile details.
- Click on share which will make HIE-CM call the expected API on HIP side.
- The successful message would be shown on app once the on-share callback is given.


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










## API Information Request Response 

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

**Download the Postman Collection** [here](/abdm-docs/Postman/scanning-hip-qr.json)

**Download the Curls** [here](/abdm-docs/Curls/scanning-hip-qr.txt)

