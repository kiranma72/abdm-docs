---
title: "By scanning HIP QR code"
date: 2022-05-07T18:00:04+05:30
weight: 1
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

1. Get patient's authentication modes relevant to specified purpose

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/fetch-modes

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
  "timestamp": "2022-05-11T09:10:08.745Z",
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

202	

Request Accepted



2. Initialize Authentication from HIP

Demographic auth mode to be used for QR code scans. Direct auth modes to be used for verbal sharing.


**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/init

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
  "timestamp": "2022-05-11T09:10:39.179Z",
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

202	

Request Accepted


3. Confirm authentication of users. Obtain linking token

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/confirm

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
  "timestamp": "2022-05-11T09:11:18.003Z",
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

202	

Request Accepted


4. Notification API in case of DIRECT mode of authentication

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/notify

**Request:** POST  

**Parameters:**

- Authorization: Access token which was issued after successful login with gateway auth server.

Type: string (header)

- X-HIP-ID: Identifier of the health information provider to which the request was intended.

Type: string (header)

- X-HIU-ID: Identifier of the health information user to which the request was intended.

Type: string (header)

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-11T09:12:07.275Z",
  "auth": {
    "transactionId": "string",
    "status": "GRANTED",
    "accessToken": "string",
    "validity": {
      "purpose": "LINK",
      "requester": {
        "type": "HIP",
        "id": 100005
      },
      "expiry": "2022-05-11T09:12:07.275Z",
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
  }
}
```

**Response:**

202	

Request Accepted



## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/shared-verbally.json)

**Download the Curls** [here](/abdm-docs/Curls/shared-verbally.txt)

