---
title: "ABHA ID Registration via Aadhaar"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---


## Overview of the functionality 

- User can register ABHA ID with their Aadhaar Number.
- To enable beneficiary registration using Aadhaar OTP, an integrator needs to generate an Aadhaar OTP, followed by OTP verification.
- Once the OTP is verified, the client is returned complete profile data along with ABHA (Health ID) Number.

**Note:** Mobile Number can be linked/verify with ABHA via using API  


## Registration via Aadhaar Number

## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![ABHA ID registration via Aadhaar](/abdm-docs/img/Creation_With_Aadhaar_on_registered_mobile_number.png)


## API Information Request Response 

1. Generate Aadhaar OTP on registrered mobile number

Api Accepts Adhar Card Number and then Generates OTP for Regestered Mobile Number

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/generateOtp

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

generateOtpRequest (body)

```json
{
  "aadhaar": "string"
}
```

**Response:** 200 OK

```json
{
  "txnId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```


2. Verify Aadhaar OTP received on registrered mobile number

Api Accepts OTP and then Checks OTP is Verified or Not

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/verifyOTP

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

**Body:**

verifyAadhaarOtp (body)

```json
{
  "otp": 812306,
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200 OK

```json
{
  "txnId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```


3.  Generate Mobile OTP for verification.

Api Accepts Mobile Number and then Creates OTP for it.

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/generateMobileOTP

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

request (body)

```json
{
  "mobile": 9545812125,
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200 OK

```json
{
  "txnId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```


4. Verify Mobile OTP in an existing transaction.

Api Accepts Mobile OTP and then Checks it is Verified or Not.

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/verifyMobileOTP

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

**Body:**

request (body)

```json
{
  "otp": 812306,
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200 OK

```json
{
  "txnId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```


5. Create Health ID using pre-verified Aadhaar & Mobile.

Api Creates HealthID using Aadhaar & Mobile Which are already Registered.

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/createHealthIdWithPreVerified

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

**Body:**

accountRequest (body)

```json
{
  "email": "string",
  "firstName": "string",
  "healthId": "string",
  "lastName": "string",
  "middleName": "string",
  "password": "string",
  "profilePhoto": "string",
  "txnId": "string"
}
```

**Response:** 200 OK

```json
{
  "authMethods": [
    "AADHAAR_OTP"
  ],
  "dayOfBirth": "string",
  "districtCode": "string",
  "districtName": "string",
  "email": "string",
  "firstName": "string",
  "gender": "string",
  "healthId": "string",
  "healthIdNumber": "string",
  "kycPhoto": "string",
  "lastName": "string",
  "middleName": "string",
  "mobile": "string",
  "monthOfBirth": "string",
  "name": "string",
  "new": true,
  "stateCode": "string",
  "stateName": "string",
  "tags": {
    "additionalProp1": "string",
    "additionalProp2": "string",
    "additionalProp3": "string"
  },
  "token": "string",
  "yearOfBirth": "string"
}
```



## Registration via Aadhaar Biometric

- To enable beneficiary registration using Aadhaar Biometric, a client needs to have a Aadhaar Registered Device (RD Device) that allows capture and processing of Biometrics of the beneficiary.
- This RD Service returns an encrypted PID block containing signed biometrics (using device private key within the registered devices secure zone) back to the calling application.
- To enable beneficiary registration using biometrics, this PID is passed in the request along with Aadhaar and other required details.
- Post verification, the client is returned complete profile data along with ABHA (Health ID).


## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![ABHA ID registration via Aadhaar](/abdm-docs/img/Creation_With_Aadhaar_Biometric.png)


## API Information Request Response 

1. Verify Aadhaar using biometrics

Api Checks Aadhaar Using Registered Biometrics.

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/verifyBio

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

**Body:**

verifyAadharOtpRequest (body)

```json
{
  "aadhaar": 31541756777,
  "bioType": "FMR",
  "pid": "PD94bWwgdmVyc2lvbj0iMS4wIj8+DQo8UGlkRGF0YT4NCiAgPFJlc3AgZXJyQ29kZT0iMCIgZXJySW5mbz0iU3VjY2VzcyIgZkNvdW50PSIxIiBmVHlwZT0iMCIgbm1Qb2ludHM9IjM5IiBxU2NvcmU9IjY4IiAvPg0KICA8RGV2aWNlSW5mbyBkcElkPSJNQU5UUkEuTVNJUEwiIHJkc0lkPSJNQU5UUkEuV0lOLjAwMSIgcmRzVmVyPSIxLjAuMyIgbWk9Ik1GUzEwMCIgbWM9Ik1JSUVHRENDQXdDZ0F3SUJBZ0lFQWdiTWdEQU5CZ2txaGtpRzl3MEJBUXNGQURDQjZqRXFNQ2dHQTFVRUF4TWhSRk1nVFdGdWRISmhJRk52Wm5SbFkyZ2dTVzVrYVdFZ1VIWjBJRXgwWkNBM01VTZXMG1SZz08L0RhdGE+DQo8L1BpZERhdGE+"
}
```

**Response:** 200 OK

```json
{
  "txnId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```



2. Create Health ID using pre-verified Aadhaar & Mobile.

Api Creates HealthID using Aadhaar & Mobile Which are already Registered.

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/createHealthIdWithPreVerified

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

**Body:**

accountRequest (body)

```json
{
  "email": "string",
  "firstName": "string",
  "healthId": "string",
  "lastName": "string",
  "middleName": "string",
  "password": "string",
  "profilePhoto": "string",
  "txnId": "string"
}
```

**Response:** 200 OK

```json
{
  "authMethods": [
    "AADHAAR_OTP"
  ],
  "dayOfBirth": "string",
  "districtCode": "string",
  "districtName": "string",
  "email": "string",
  "firstName": "string",
  "gender": "string",
  "healthId": "string",
  "healthIdNumber": "string",
  "kycPhoto": "string",
  "lastName": "string",
  "middleName": "string",
  "mobile": "string",
  "monthOfBirth": "string",
  "name": "string",
  "new": true,
  "stateCode": "string",
  "stateName": "string",
  "tags": {
    "additionalProp1": "string",
    "additionalProp2": "string",
    "additionalProp3": "string"
  },
  "token": "string",
  "yearOfBirth": "string"
}
```



## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)



