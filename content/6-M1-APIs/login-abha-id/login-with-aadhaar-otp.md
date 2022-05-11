---
title: "Login with Aadhaar OTP"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---

## Login with Aadhaar OTP

## Overview of the functionality 

- An OTP is triggered with the Aadhaar linked mobile number of the patient. 
- The patient must provide the OTP to the user to complete the authentication


## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![Login ABHA ID via Aadhaar Otp](/abdm-docs/img/Login_With_ABHA_using_mobile.png)



## API Information Request Response 

1. Auth token public key

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/auth/cert

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

