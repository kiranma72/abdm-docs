---
title: "ABHA ID Registration via Other Documents"
date: 2022-05-07T18:00:04+05:30
weight: 2
draft: false
---

## ABHA ID Registration via Other Documents

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



**1. Generate the Gateway session**

Bearer token is received as part of respose and should be passed a Authorization token for subsequent API calls.

**URL:** https://dev.ndhm.gov.in/gateway/v0.5/sessions

**Request:** POST  

**Body:**

```json
{
    "clientId": "string",
    "clientSecret": "string",
    "grantType": "client_credentials"
}
```

**Response:** 200 OK

```json
{
    "accessToken": "string",
    "expiresIn": 600,
    "refreshExpiresIn": 1800,
    "refreshToken": "string",
    "tokenType": "bearer"
}
```





**2. Authentication token public certificate. This certificate is also used to encrypt the data.**

**URL:** https://healthidsbx.abdm.gov.in/api/v1/auth/cert

**Request:** GET  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)


**Response:** 200  OK

string




**3. Api Accepts Mobile Number and creates OTP for it**

**URL:** https://healthidsbx.abdm.gov.in/api/v2/document/generate/mobile/otp

Explanation - Api Accepts Mobile Number and creates OTP fo it.

Request Body - Required

Responce - Api Accepts Mobile Number and creates OTP fo it. Returns Error for Invalid Mobile number.


**Request:** POST  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)


**Body:**

generateOtpRequest (body)

```json
{
  "mobile": "9545812125"
}
```

**Response:** 200 OK

```json
{
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```



**4. Api Accepts Mobile OTP and validates it**

**URL:** https://healthidsbx.abdm.gov.in/api/v2/document/verify/mobile/otp

Explanation - Api Accepts Mobile OTP and validates it.

Request Body - Required

Responce - Api Accepts Mobile OTP and validates it. Returns Error for Invalid Mobile OTP.


**Request:** POST  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)


**Body:**

verifyMobileWebRequest  (body)

```json
{
  "otp": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI=",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 200 OK

```json
{
  "token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
}
```



**5. Validate the document**

Match the provided demographic details (Name, DOB, Gender) against the document. It also checks for already created ABHA Number or Enrolment number against the document

Explanation - API accepts Identity Document details and validates the document. Match the provided demographic details (Name, DOB, Gender) against document. It also check for the already created ABHA Number or Enrolment number against the document.

Request Body - Required

Response - API accepts Identity Document details and validates the document. Match the provided demographic details(Name, DOB, Gender) against document. It also check for the already created ABHA Number or Enrolment number against the document. Returns Error for Invalid Identity Document details.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/document/validate

**Request:** POST  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)


**Body:**

request (body)

```json
{
  "dayOfBirth": "21",
  "documentNumber": "UK0720190567",
  "documentType": "DRIVING_LICENCE",
  "firstName": "Deepak",
  "gender": "M",
  "lastName": "Pant",
  "middleName": "Kumar",
  "monthOfBirth": "03",
  "yearOfBirth": "1990"
}
```

**Response:** 200 OK

```json
{
  "address": "b-14 someshwar nagar",
  "enrolmentNumber": "43-4231-5504-6839",
  "healthIdNumber": "43-4221-5105-6749",
  "jwtResponse": {
    "expiresIn": 1800,
    "refreshExpiresIn": 86400,
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
  },
  "verification": {
    "fields": [
      {
        "key": "1255477819",
        "matched": true
      }
    ],
    "matched": true
  }
}
```



**6.  Create ABHA Number using ID documents like Driving Licence, PAN Card**

Explanation - Api Accepts Identity Document details and Creates HealthID for it.

Request Body - Required

Responce - Api Accepts Identity Document details and Creates HealthID for it. Returns Error for Invalid Identity Document details.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/document

**Request:** POST  

**Parameters:**

- Authorization
string (header)

- X-HIP-ID
string (header)

- T-Token
string (header)

**Body:**

request (body)	

```json
{
  "address": "Street No 3, Opp. gali no 2",
  "dayOfBirth": "04",
  "districtCode": "401",
  "documentNumber": "UK0720190567",
  "documentType": "DRIVING_LICENCE",
  "firstName": "Deepak",
  "gender": "M",
  "lastName": "Pant",
  "middleName": "Kumar",
  "mobile": "9545812125",
  "monthOfBirth": "03",
  "photo": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkJCQkJCQoLCwoODw0PDhQSERESFB4WFxYXFh4uHSEdHSEdLikxKCUoMSlJOTMzOUlUR0NHVGZbW2aBeoGoqOIBCQkJCQkJCgsLCg4PDQ8OFBIRERIUHhYXFhcWHi4dIR0dIR0uKTEoJSgxKUk5MzM5SVRHQ0dUZltbZoF6gaio4v/CABEIBLAHgAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwABBAUGB//aAAgBAQAAAADwawLpMspcK7qrlE5F0Vtul2bVywMUNeBHUkW/bmxvYELGuNjh2VDvixxo5ViljKjDRMoahCULjs2JCShjhjh2OGxo0Y2MoXHOLszsKLhw7tD99mpZQxj8xceofmLEKFwXLTIyHwY1Ls+iEotjHY0M0pjRYxtGj4VFKLPohQlFQyy4Qipc0XG9pS+CP/2Q==",
  "photoBack": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkJCQkJCQoLCwoODw0PDhQSERESFB4WFxYXFh4uHSEdHSEdLikxKCUoMSlJOTMzOUlUR0NHVGZbW2aBeoGoqOIBCQkJCQkJCgsLCg4PDQ8OFBIRERIUHhYXFhcWHi4dIR0dIR0uKTEoJSgxKUk5MzM5SVRHQ0dUZltbZoF6gaio4v/CABEIBLAHgAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwABBAUGB//aAAgBAQAAAADwawLpMspcK7qrlE5F0Vtul2bVywMUNeBHUkW/bmxvYELGuNjh2VDvixxo5ViljKjDRMoahCULjs2JCShjhjh2OGxo0Y2MoXHOLszsKLhw7tD99mpZQxj8xceofmLEKFwXLTIyHwY1Ls+iEotjHY0M0pjRYxtGj4VFKLPohQlFQyy4Qipc0XG9pS+CP/2Q==",
  "stateCode": "27",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "yearOfBirth": "1990"
}
```


**Response:** 200 OK

```json
{
  "address": "b-14 someshwar nagar",
  "authMethods": "AADHAAR_OTP",
  "dayOfBirth": "31",
  "districtCode": "401",
  "documentNumber": "UK0720190567",
  "documentPhoto": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkJCQkJCQoLCwoODw0PDhQSERESFB4WFxYXFh4uHSEdHSEdLikxKCUoMSlJOTMzOUlUR0NHVGZbW2aBeoGoqOIBCQkJCQkJCgsLCg4PDQ8OFBIRERIUHhYXFhcWHi4dIR0dIR0uKTEoJSgxKUk5MzM5SVRHQ0dUZltbZoF6gaio4v/CABEIBLAHgAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwABBAUGB//aAAgBAQAAAADwawLpMspcK7qrlE5F0Vtul2bVywMUNeBHUkW/bmxvYELGuNjh2VDvixxo5ViljKjDRMoahCULjs2JCShjhjh2OGxo0Y2MoXHOLszsKLhw7tD99mpZQxj8xceofmLEKFwXLTIyHwY1Ls+iEotjHY0M0pjRYxtGj4VFKLPohQlFQyy4Qipc0XG9pS+CP/2Q==",
  "documentType": "DRIVING_LICENCE",
  "firstName": "Deepak",
  "gender": "M",
  "healthId": "deepakndhm",
  "healthIdNumber": "43-4221-5105-6749",
  "lastName": "singh",
  "middleName": "kumar",
  "mobile": "9545812125",
  "monthOfBirth": "05",
  "name": "kishan kumar singh",
  "photo": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkJCQkJCQoLCwoODw0PDhQSERESFB4WFxYXFh4uHSEdHSEdLikxKCUoMSlJOTMzOUlUR0NHVGZbW2aBeoGoqOIBCQkJCQkJCgsLCg4PDQ8OFBIRERIUHhYXFhcWHi4dIR0dIR0uKTEoJSgxKUk5MzM5SVRHQ0dUZltbZoF6gaio4v/CABEIBLAHgAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwABBAUGB//aAAgBAQAAAADwawLpMspcK7qrlE5F0Vtul2bVywMUNeBHUkW/bmxvYELGuNjh2VDvixxo5ViljKjDRMoahCULjs2JCShjhjh2OGxo0Y2MoXHOLszsKLhw7tD99mpZQxj8xceofmLEKFwXLTIyHwY1Ls+iEotjHY0M0pjRYxtGj4VFKLPohQlFQyy4Qipc0XG9pS+CP/2Q==",
  "photoBack": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkJCQkJCQoLCwoODw0PDhQSERESFB4WFxYXFh4uHSEdHSEdLikxKCUoMSlJOTMzOUlUR0NHVGZbW2aBeoGoqOIBCQkJCQkJCgsLCg4PDQ8OFBIRERIUHhYXFhcWHi4dIR0dIR0uKTEoJSgxKUk5MzM5SVRHQ0dUZltbZoF6gaio4v/CABEIBLAHgAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwABBAUGB//aAAgBAQAAAADwawLpMspcK7qrlE5F0Vtul2bVywMUNeBHUkW/bmxvYELGuNjh2VDvixxo5ViljKjDRMoahCULjs2JCShjhjh2OGxo0Y2MoXHOLszsKLhw7tD99mpZQxj8xceofmLEKFwXLTIyHwY1Ls+iEotjHY0M0pjRYxtGj4VFKLPohQlFQyy4Qipc0XG9pS+CP/2Q==",
  "state": "MH",
  "stateCode": "27",
  "stateName": "MAHARASHTRA",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "verificationStatus": "verified",
  "verificationType": "testing",
  "yearOfBirth": "1994"
}
```




## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/ABHA_Registration_Via_OtherDocuments.json)

**Download the Curls** [here](/abdm-docs/Curls/)



