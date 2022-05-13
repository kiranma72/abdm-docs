---
title: "Retrieve ABHA via Aadhaar OTP"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---


## Retrieve ABHA via Aadhaar OTP

## Overview of the functionality 

- To retrieve ABHA (Health ID), an OTP is sent on a registered mobile number and the user's health ID is retrieved from the ABDM server.
- The sequence of APIs used via this method is shown in the diagram below. 

## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![Login ABHA ID via Aadhaar Otp](/abdm-docs/img/Forgot_ABHA(Health_ID)_Retrieve_via_Aadhaar_OTP.png)


## API Information Request Response 


1. Generate Aadhaar OTP on Registered mobile number

Explanation - API accepts Aadhaar Number and then generates OTP for linked number as part of Forgot flow.

Request Body - Required

Response - Api Accepts Aadhaar Number and then generates OTP for linked number as part of Forgot flow. Returns Transaction ID.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/forgot/healthId/aadhaar/generateOtp

**Need to confime whether API is v1 or v2 in pdf API is mentioned as v2**

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

generateOtpRequest  (body)

```json
{
  "aadhaar": "31541756999"
}
```

**Response:** 200

```json
{
  "mobileNumber": "XXXXXX2125",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```



2. Verify aadhar OTP sent as part of forget ABHA Number

Explanation - API accepts OTP and then checks is it Valid as per given Aadhaar Transaction.

Request Body - Required

Responce - Api Accepts OTP then returns ABHA Number and ABHA Address accordingly.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/forgot/healthId/aadhaar

**Need to confime whether API is v1 or v2 in pdf API is mentioned as v2**

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

authAccountAadhaarOTPRequest  (body)

```json
{
  "otp": "816406",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200

```json
{
  "healthId": "deepak.pant",
  "healthIdNumber": "43-4221-5105-6749"
}
```


## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)



