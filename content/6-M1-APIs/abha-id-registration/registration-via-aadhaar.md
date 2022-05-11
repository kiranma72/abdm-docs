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

[ABHA ID registration via Aadhaar](/abdm-docs/img/Creation_With_Aadhaar_on_registered_mobile_number.png)


## API Information Request Response 

1. Generate Aadhaar OTP on registrered mobile number

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/generateOtp

**Request:** POST  

**Parameters:**

- Authorization: Access token which was issued after successful login with gateway auth server.

Type: string (header)


**Body:**

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

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/verifyOTP

**Request:** POST  

**Parameters:**

- Authorization: Access token which was issued after successful login with gateway auth server.

Type: string (header)


**Body:**

```json
{
  "otp": "string",
  "restrictions": "string",
  "txnId": "string"
}
```

**Response:** 200 OK

```json
{
  "txnId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```


3.  Generate Mobile OTP to verify mobile number.

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/generateMobileOTP

**Request:** POST  

**Parameters:**

- Authorization: Access token which was issued after successful login with gateway auth server.

Type: string (header)


**Body:**

```json
{
  "mobile": "string",
  "txnId": "string"
}
```

**Response:** 200 OK

```json
{
  "txnId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```


4. Verify Mobile OTP in an existing transaction.

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/verifyMobileOTP

**Request:** POST  

**Parameters:**

- Authorization: Access token which was issued after successful login with gateway auth server.

Type: string (header)


**Body:**
```json
{
  "otp": "string",
  "txnId": "string"
}
```

**Response:** 200 OK

```json
{
  "txnId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```


5. Create Health ID using pre-verified Aadhaar & Mobile.

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/createHealthIdWithPreVerified

**Request:** POST  

**Parameters:**

- Authorization: Access token which was issued after successful login with gateway auth server.

Type: string (header)


**Body:**

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

[ABHA ID registration via Aadhaar](/abdm-docs/img/Creation_With_Aadhaar_Biometric.png)



## API Information Request Response 

1. Verify Aadhaar using biometrics

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/verifyBio

**Request:** POST  

**Parameters:**

- aadhaar
string (query)

- pid
string (query)

- restrictions
string (query)

**Body:**

```json

```

**Response:** 200 OK

```json
{
  "txnId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```


1. Verify Aadhaar using biometrics

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/verifyBio

**Request:** POST  

**Parameters:**

- aadhaar
string (query)

- pid
string (query)

- restrictions
string (query)

**Body:**

```json

```

**Response:** 200 OK

```json
{
  "txnId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```


2. Create Health ID using pre-verified Aadhaar & Mobile.

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/registration/aadhaar/createHealthIdWithPreVerified

**Request:** POST  

**Parameters:**

- Authorization: Access token which was issued after successful login with gateway auth server.

Type: string (header)


**Body:**

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



