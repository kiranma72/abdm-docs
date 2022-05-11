---
title: "ABHA ID Registration via Other Documents"
date: 2022-05-07T18:00:04+05:30
weight: 2
draft: false
---

## Registration via Other Documents

## Overview of the functionality 

- Currently we support Driving License (DL) & PAN for ABHA number generation, apart from Aadhaar. 
- ABDM plans to roll out other ID documents as well to enable creation.
- The same will be communicated and updated in the documentation as necessary.
- However, the integration flow will remain as the DL/PAN flow. 
- To enable beneficiary registration using other documents, the user is requested his/her mobile number to be linked with ABHA (Health ID) Number.
- An OTP is sent to the given mobile number and after verifying the OTP , demographic information of the user is captured along with the driving license number . 
- Following demographic details are expected from the end user
   - Name
   - Date of birth
   - Gender

- The submitted demographic details are then matched against the DL/PAN database.
- ABHA system also checks the details against the existing ABHA (Health ID) or Enrolment number database to prevent duplication.
- Users are requested to upload scanned front and back images of their DL/PAN.
- Post submission, an enrollment number is generated.
- Health care workers/Facility Managers are expected to ensure that the submitted DL/PAN is of the end user requesting creation of ABHA.
- They can ensure the same by matching the picture in the uploaded document with the requesting person.


Please note, ABHA creation via Aadhaar is a one step process wherein, ABHA is created instantaneously. However, in case of other ID documents, an enrollment 
number is generated first which can only be converted to ABHA once a manual verification of identity is complete. 


ABHA (Health ID) created through Self mode via using Driving license/PAN, an 
Enrolment number has been issued which can be verified at any facility centers.


**Note:** ABDM will soon roll out features that will support ABHA (Health ID) creation with other ID documents such as PAN card, Driving License, etc. in assisted mode at 
participating health facilities.


## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.

![ABHA ID registration via Aadhaar](/abdm-docs/img/Creation_With_Other_Document.png)



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

**URL:** https://healthidsbx.ndhm.gov.in/api/

**Request:** POST  

**Parameters:**

- Authorization: Access token which was issued after successful login with gateway auth server.

Type: string (header)


**Body:**

```json

```

**Response:** 200 OK

```json

```


2. Create Health ID using pre-verified Aadhaar & Mobile.

**URL:** https://healthidsbx.ndhm.gov.in/api/

**Request:** POST  

**Parameters:**

- Authorization: Access token which was issued after successful login with gateway auth server.

Type: string (header)


**Body:**

```json

```

**Response:** 200 OK

```json

```



## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)



