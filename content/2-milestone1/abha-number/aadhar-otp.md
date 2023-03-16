+++
title = "Using Aadhaar OTP"
date = 2023-03-16T09:30:25+05:30
weight = 1
chapter = true
pre = "<b>2.1.1 </b>"
+++

# Registration via Aadhaar Linked Number & OTP

### Functionality Overview 

- User can register ABHA ID with their Aadhaar registered contact number.
- To enable beneficiary registration using Aadhaar OTP, an integrator needs to generate an Aadhaar OTP, followed by OTP verification.
- Once the OTP is verified, the client is returned complete profile data along with ABHA (Health ID) Number.

**Note:** Mobile Number can be linked/verify with ABHA via using API  


### API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![ABHA ID registration via Aadhaar](/abdm-docs/img/Creation_With_Aadhaar_on_registered_mobile_number.png)

### API Information Request Response 

**1. Generate the Gateway session**

Bearer token is received as part of respose and should be passed a Authorization token for subsequent API calls.

**URL:** https://dev.ndhm.gov.in/gateway/v0.5/sessions

**Request:** POST  

**Body:**

```json
{
    "clientId": "your-clientID",
    "clientSecret": "your-clientSecret",
    "grantType": "client_credentials"
}
```

**Response:** 200 OK

```json
{
    "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJBbFJiNVdDbThUbTlFSl9JZk85ejA2ajlvQ3Y1MXBLS0ZrbkdiX1RCdkswIn0.eyJleHAiOjE2NTMzNjkyNTYsImlhdCI6MTY1MzM2ODY1NiwianRpIjoiZDg5YTFlYmUtZWRlNS00Y2U4LWEwZTAtMTUzNGNjNzkyYjk0IiwiaXNzIjoiaHR0cHM6Ly9kZXYubmRobS5nb3YuaW4vYXV0aC9yZWFsbXMvY2VudHJhbC1yZWdpc3RyeSIsImF1ZCI6WyJyZWFsbS1tYW5hZ2VtZW50IiwiYWNjb3VudCJdLCJzdWIiOiIwNmJkNGZlNy04NjEyLTRiZmEtYTI1NS1iMDdiZmFjZmU1M2QiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJoZWFsdGhpZC1hcGkiLCJzZXNzaW9uX3N0YXRlIjoiNjU2NGY2N2UtZjM4My00NGRiLWIyOTYtNDA2ZmE2MmVj",
    "expiresIn": 600,
    "refreshExpiresIn": 1800,
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICIyMWU5NzA4OS00ZTcxLTQyNGEtOTAzYS1jOTAyMWM1NmFlNWYifQ.eyJleHAiOjE2NTMzNzA0NTYsImlhdCI6MTY1MzM2ODY1NiwianRpIjoiNGY1ZjZjMWYtYTk0Yy00ZjJmLThmZjctYTY2MDRiN2M2ZjJhIiwiaXNz",
    "tokenType": "bearer"
}
```

**2. Generate Aadhaar OTP on registrered mobile number**

Api Accepts Adhar Card Number and then Generates OTP for Regestered Mobile Number

**URL:** https://healthidsbx.abdm.gov.in/api/v1/registration/aadhaar/generateOtp

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

generateOtpRequest (body)

```json
{
  "aadhaar": "31541756999"
}
```

**Response:** 200 OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```


**3. Verify Aadhaar OTP received on registrered mobile number**

Api Accepts OTP and then Checks OTP is Verified or Not

**URL:** https://healthidsbx.abdm.gov.in/api/v1/registration/aadhaar/verifyOTP

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

**Body:**

verifyAadhaarOtp (body)

```json
{
  "otp": "812306",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200 OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```


**4.  Generate Mobile OTP for verification.**

Api Accepts Mobile Number and then Creates OTP for it.

**URL:** https://healthidsbx.abdm.gov.in/api/v1/registration/aadhaar/generateMobileOTP

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)


**Body:**

request (body)

```json
{
  "mobile": "9545812125",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200 OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```


**5. Verify Mobile OTP in an existing transaction.**

Api Accepts Mobile OTP and then Checks it is Verified or Not.

**URL:** https://healthidsbx.abdm.gov.in/api/v1/registration/aadhaar/verifyMobileOTP

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

**Body:**

request (body)

```json
{
  "otp": "812306",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200 OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```


**6. Create ABHA Number using pre-verified Aadhaar & Mobile.**

API creates ABHA Number using Aadhaar & Mobile Which are already Registered.

**URL:** https://healthidsbx.abdm.gov.in/api/v1/registration/aadhaar/createHealthIdWithPreVerified

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

**Body:**

accountRequest (body)

```json
{
  "email": "ram@Demo.com",
  "firstName": "abhi",
  "healthId": "test",
  "lastName": "A",
  "middleName": "ram",
  "password": "India@143",
  "profilePhoto": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkJCQkJCQoLCwoODw0PDhQSERESFB4WFxYXFh4uHSEdHSEdLikxKCUoMSlJOTMzOUlUR0NHVGZbW2aBeoGoqOIBCQkJCQkJCgsLCg4PDQ8OFBIRERIUHhYXFhcWHi4dIR0dIR0uKTEoJSgxKUk5MzM5SVRHQ0dUZltbZoF6gaio4v/CABEIBLAHgAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwABBAUGB//aAAgBAQAAAADwawLpMspcK7qrlE5F0Vtul2bVywMUNeBHUkW/bmxvYELGuNjh2VDvixxo5ViljKjDRMoahCULjs2JCShj",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200 OK

```json
{
    "token": "string",
    "refreshToken": "string",
    "healthIdNumber": "12-3456-7899-1111",
    "name": "Ram",
    "gender": "M",
    "yearOfBirth": "1977",
    "monthOfBirth": "1",
    "dayOfBirth": "1",
    "firstName": "abhi",
    "healthId": "test@sbx",
    "lastName": "A",
    "middleName": "ram",
    "stateCode": "27",
    "districtCode": "",
    "stateName": "MAHARASHTRA",
    "districtName": "Pune",
    "email": "ram@Demo.com",
    "kycPhoto": null,
    "profilePhoto": "",
    "mobile": "1234567890",
    "authMethods": [
        "AADHAAR_BIO",
        "AADHAAR_OTP",
        "DEMOGRAPHICS",
        "PASSWORD",
        "MOBILE_OTP"
    ],
    "pincode": null,
    "tags": {},
    "new": true
}
```

### Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/ABHA_Registration_Via_Aadhaar.json)

**Download the Curls** [here](/abdm-docs/Curls/)


