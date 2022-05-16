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
- The HIE-CM will verify this is a registered healthcare provider and identify the HRP linked to this HIP in the ABDM registry 
- The Gateway will call the share-profile api on the callback URL registered for this HRP
- The HRP software must create a screen to display all the scanned profiles for a (counter) code
- The operator (at a counter) should be able to select a shared profile and perform a fast user registration 
- Remember to correctly handle this for both new and returning patients

![Scan HIP QR Code](../scan-hip-qr.png)


## Create a QR code for your Health Facility
=======
- Patient must have a PHR app and have a valid PHR address.
- Hospital must generate a HIP QR code and display it at the registration counter.

Generate a QR code for the data in below format. You can use something like [Sample QR Generator](https://www.the-qrcode-generator.com/). ABDM will shortly release a QR code generator that can be used.

Your HIP ID is the same as the Health Facility Registry ID. You must have linked this HIP ID to your HRP

```json
{
    "hipId": "HFR1010342452",
    "code": "any information you want to get back with the scan, e,g counterId, Dept Id"
}
```

- Go to ABHA Mobile Application, then My Profile and Find Scan option on the top right.
- Scan the QR code, the app should fetch details of QR code along with User profile details.
- Click on share which will make HIE-CM call the expected API on HIP side.
- The successful message would be shown on app once the on-share callback is given.


## API Sequence 

![Scan HIP QR Code API Seq](../share-profile-hip-qr-api-seq.png)
=======

### 1. User's Profile is shared with the HRP 

**URL:** {HRP CALLBACK URL}/v0.5/patients/profile/share
**Request:** POST  
**HEADERS:**
- Authorization: JWT Token from Gateway
- X-HIP-ID: hipID that was embedded in the QR code
**Body:**
```json
{
  "requestId": "499a5a4a-7dda-4f20-9b67-e24589627061",
  "timestamp": "2022-05-10T14:19:12.993Z",
  "profile": {
    "hipCode": "12345 (CounterId)",
    "patient": {
      "healthId": "test@sbx",
      "healthIdNumber": "1111-1111-1111-11",
      "name": "Jane Doe",
      "gender": "F",
      "address": {
        "line": "string",
        "district": "string",
        "state": "string",
        "pincode": "string"
      },
      "yearOfBirth": 2000,
      "dayOfBirth": 27,
      "monthOfBirth": 02,
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

202	Request Accepted

> Swagger URL:  https://sandbox.abdm.gov.in/swagger/ndhm-hip.yaml See the Profile Section

Note that "healthId": contains the PHR address of the user and "healthIdNumber": contains the linked ABHA no for this PHR address. You need to save the PHR address for the user in your application. You can use the other information provided to quickly register the user.

"hipCode": will contain whatever you put in "code" as part of the QR 

### 2. Responsed to patient's share profile request

**URL:** POST https://dev.abdm.gov.in/gateway/v0.5/patients/profile/on-share
**Request:**   
**HEADERS:**
- Authorization: JWT Sessions token 
- X-CM-ID: Should be the domain in the PHR Address - @sbx or @abdm
**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-11T04:58:00.037Z",
  "acknowledgement": {
    "status": "SUCCESS",
    "healthId": "test@sbx"
  },
  "error": {
    "code": 1000,
    "message": "string"
  },
  "resp": {
    "requestId": "499a5a4a-7dda-4f20-9b67-e24589627061"
  }
}
```

**Response:**

202	Request Accepted

Ensure that the contents of  "healthID" and "requestID" match the information you got in the share request. 

If there is an issue with the share, set the "status" to ERROR and provide a clear error message with what went wrong. This will be sent back to the PHR app and displayed to the user 


### 3. Initiate a demographic auth to verify the PHR address and obtain a linking token

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/init
**Request:** POST  
**HEADERS:**
- Authorization: JWT Sessions token 
- X-CM-ID: Should be the domain in the PHR Address - sbx or abdm
**Body:**
```json
{
  "requestId": "28ac1de6-a2ce-4b8e-8afe-a97f7bb52b85",
  "timestamp": "2022-05-15T15:16:47.21234",
  "query": {
    "id": "test@sbx",
    "purpose": "LINK",
    "authMode": "DEMOGRAPHICS",
    "requester": {
      "type": "HIP",
      "id": HFR1010342452
    }
  }
}
```

**Response:**

202	  Accepted


### 4. Recieve the response to PHR address verification request

**URL:** {HRP CALLBACK URL}/v0.5/users/auth/on-init
**Request:** POST  
**HEADERS:**
- Authorization: GW JWT token 
- X-HIP-ID: Same HIP id that was passed in the auth init 
**Body:**

```json
{
  "requestId": "62f31135-7e5b-4714-9a81-4fdcfced2651",
  "timestamp": "2022-05-15T15:16:48.277264",
  "auth": {
    "transactionId": "ee1d6495-96a3-4fb6-a0fc-f5b33e3e0434",
    "mode": "DEMOGRAPHICS",
    "meta": {
      "hint": null,
      "expiry": "2022-05-15T17:16:48.277271"
    }
  },
  "error": null,
  "resp": {
    "requestId": "28ac1de6-a2ce-4b8e-8afe-a97f7bb52b85"
  }
}
```

**Response:**
202	 Accepted


### 5. Send the demographics for confirmation 

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/confirm
**Request:** POST  
**HEADERS:**
- Authorization: JWT Session Token
- X-CM-ID: The domain in the phr address, sbx or abdm

**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-15T15:16:49.87345",
  "transactionId": "ee1d6495-96a3-4fb6-a0fc-f5b33e3e0434",
  "credential": {
    "demographic": {
      "name": "Jane Doe",
      "gender": "F",
      "dateOfBirth": "2000-02-27"
    }
  }
}
```

**Response:**

202	  Accepted

Ensure transaction ID is the same as that recieved in the on-init call. Share the demographics exactly as you got in the profile that was shared. You can send the month / day as 01 if only the year of birth is available as part of dateOfBirth. example "2000-01-01"


6. Get and Save the linking token for this user

**URL:** {HRP Callback URL}/v0.5/users/auth/on-confirm
**Request:** POST  
**Parameters:**
- Authorization  Gateway token
- X-HIP-ID  Same that was passed as HIP ID in auth init 

- X-HIU-ID  string (header)

**Body:**

```json
{
  "requestId": "9ccbe503-f87a-4f9b-8a0e-d8691d1c9bc3",
  "timestamp": "2022-05-16T12:39:48.906988",
  "auth": {
    "accessToken": "eyJhbGciOiJSUzUxMiJ9.eyJzdWIiOiJraXJhbm1hQHNieCIsInJlcXVlc3RlclR5cGUiOiJISVAiLCJyZXF1ZXN0ZXJJZCI6IktULUhJUCIsInBhdGllbnRJZCI6ImtpcmFubWFAc2J4Iiwic2Vzc2lvbklkIjoiZWIyNjdhY2UtYTk2NS00MzRjLWJlNjEtYzcyYjA0ZTNhOWM0IiwiZXhwIjoxNjUyNzkxMTg4LCJpYXQiOjE2NTI3MDQ3ODh9.DAPKgCigF_rOh-OFJocizsOlawDGnCZNDLvzW6HQswR6u30LzDOyJ_JMbW_8-owH0X-e-GCy-zpaiLDxWaVihDOrc51J7Aps-aeDa-sW8r7jspYCOQp0gyT3CzXl-GIkqiaHjCnHTdu5RA4oMGtGTfXKgpZtSsY5PROsekOFFTDlA3BtXnCd1iSdubdbihPtEKL90-w3PCAdm8gYQql8FaxCmMEcsQnNFn-YqqPwq32BSjbmlS6bEmuUpkWnIpXFcpO4GFvQo4VXRlqSFjFu5cjhi8XA61C1cdxCumv7N4uEEq7DPqJ69JCeY48AakWESAEjuP2pxBPhn8520q4gTg",
    "patient": null
  },
  "error": null,
  "resp": {
    "requestId": "b40fb334-6e22-4bee-8269-bc11b2453d7a"
  }
}
```

**Response:**

202	 Accepted

The "accessToken" in this response is also reffered to as "linking token". This is a one time use token and does not expire till you use it to link a health record with this PHR address. You can save this in your application till you have a new health record available for you to link 


If there is any mismatch between the PHR Address (sent in init) and the demographics (send in confirm) you will get a response that looks like 

```json
{
  "requestId": "a1882f39-f507-4dfa-8275-fdc275403f4b",
  "timestamp": "2022-05-16T12:31:01.361004",
  "auth": null,
  "error": {
    "code": 1441,
    "message": "Invalid auth confirm request."
  },
  "resp": {
    "requestId": "22c16352-e66b-4cb0-8330-08234957ac55"
  }
}
```

**Response:**

202	 Accepted

## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/scanning-hip-qr.json)

**Download the Curls** [here](/abdm-docs/Curls/scanning-hip-qr.txt)

