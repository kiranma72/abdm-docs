---
title: "By scanning PHR Address QR"
date: 2022-05-07T18:00:04+05:30
weight: 2
draft: false
---

## Overview of the functionality 
- Patient must have a PHR app with a valid PHR address or physical card like a ABHA card
- Hospital must have a 2D Barcode scanner available at the registration counter
- The HRP software registration page have text box to load data scanned from PHR QR Code.
- Hospital operator scans the QR code on patient PHR card or as displayed in PHR mobile App
- The Patient details like PHR address, Name, DOB, Gender, State Id, District Id, etc are embedded in the QR code as a JSON
- HRP software must validate the scanned data and collect a linking token from ABDM
- THe software must use the information scanned to register the patient and save the PHR Address

## Example QR Codes 

**QR Codes in PHR Apps**
![PHR App QR Code](../phrqr-in-app.png)

```json
{   
  "hidn":"42-7175-8604-4553",
  "phr":"kiranma@sbx",
  "name":"Kiran Anandampillai",
  "gender":"M",
  "statelgd":"4",
  "distlgd":"44",
  "dob":"xx-9-19xx",
  "address":"As declared by the user"
}
```
Please note that "hidn" is available only if the PHR address has been linked with a ABHA


**QR Code in ABHA card**
![ABHA card example](../abha-card-eg.png)

```json
{
  "hidn":"15-3638-0684-6247",
  "hid":"kiranma@abdm",
  "name":"Kiran Mandyam Anandampillai",
  "gender":"M",
  "statelgd":"29",
  "distlgd":"-",
  "dob":"xx/9/19xx",
  "state name":"Karnataka",
  "district_name":"Bengaluru",
  "mobile":"984x1x2x6x",
  "address":"C/O father name # door no, as from the KYC document"
}
```
Please note that HID is populated only if the user has downloaded a PHR app and chosen a PHR address. If not, use 14digit-hidn@sbx or @abdm as the PHR address 


## API Sequence 

Same as steps for demographic auth and confirmation in [Scanning HIP QR](../scanning-hip-qr2/#api-sequence)

## API Information Request Response 

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

202   Accepted


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
202  Accepted


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

202   Accepted

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

202  Accepted

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

202  Accepted


## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/scanning-phraddr.json)

**Download the Curls** [here](/abdm-docs/Curls/scanning-phraddr.txt)

