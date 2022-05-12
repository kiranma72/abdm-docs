---
title: "Login to your ABHA using Mobile"
date: 2022-05-07T18:00:04+05:30
weight: 3
draft: false
---

## Login to your ABHA using Mobile

## Overview of the functionality 

- Users will now be able to login to their ABHA using their Mobile Number. 
- In case multiple ABHA numbers are linked to a Mobile Number, users will be able to choose the account they want to login to. 
- The patient must provide the OTP to the user to complete the authentication.
- To begin the process, the Authentication token public certificate API (V1.Auth/cert) is called.
- After that An OTP is sent to the patient’s mobile number that is linked with the ABHA.
- The patient must share the OTP with the user for verification.
- A token has been returned and can be used for Profile APIs purpose.


## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![Login ABHA ID via Aadhaar Otp](/abdm-docs/img/Login_With_ABHA_using_mobile.png)


## API Information Request Response 

1. Auth token public key

**URL:** https://healthidsbx.ndhm.gov.in/api/

**Request:** GET  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)


**Body:**

```json

```

**Response:** 200 OK

```json
string
```





## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)

