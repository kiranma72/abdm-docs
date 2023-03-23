+++
title = "Using Driving License"
date = 2023-03-16T09:30:25+05:30
weight = 4
chapter = true
pre = "<b>2.1.4 </b>"
+++


# ABHA ID Registration via Driving Licence


## Overview of the functionality

{{%icon icon="hand-point-right" %}} Currently ABDM support Driving License (DL) for ABHA number generation, apart from Aadhaar. 

{{%icon icon="hand-point-right" %}} To enable beneficiary registration using other documents, the user is requested his/her mobile number to be linked with ABHA Number.

{{%icon icon="hand-point-right" %}} An OTP is sent to the given mobile number and after verifying the OTP , demographic information of the user is captured along with the driving license number . 

{{%icon icon="hand-point-right" %}} Following demographic details are expected from the end user
   - Name
   - Date of birth (DOB)
   - Gender

{{%icon icon="hand-point-right" %}} The submitted demographic details are then matched against the DL database.

{{%icon icon="hand-point-right" %}} ABHA system also checks the details against the existing ABHA or Enrolment number database to prevent duplication.

{{%icon icon="hand-point-right" %}} Users are requested to upload scanned front and back images of their DL.

{{%icon icon="hand-point-right" %}} Post submission, an enrollment number is generated.

{{%icon icon="hand-point-right" %}} Health care workers/Facility Managers are expected to ensure that the submitted DL is of the end user requesting *creation of ABHA.*

{{%icon icon="hand-point-right" %}} They can ensure the same by matching the picture in the uploaded document with the requesting person.

{{% notice %}} ABHA creation via Aadhaar is a one step process wherein, ABHA is created instantaneously. However, in case of other ID documents, an enrollment 
number is generated first which can only be converted to ABHA once the manual verification of identity is complete. 

ABHA created through Self mode via using Driving license, an 
Enrolment number has been issued which can be verified at any facility centers.
{{% /notice %}}

*Documents Required* – Since this process is online, the ABHA registration will not require you to submit any documents physically. However, since the user will have to enter the details and some important information for proper verification, the user will need:

{{%icon icon="arrow-right" %}} His/Her active mobile number

{{%icon icon="arrow-right" %}} Driving license number (only for the generation of the enrollment number)

## Sample User Experience
- Site: https://abha.abdm.gov.in/ 
![initial_page](../register_via_dl.gif)
![dl_login_validate_via_otp_page](../dl_validate_via_otp.gif)
![verify_dl_for_abha_number_reg](../verify_dl_for_ABHA_number.png)

## ABHA OTP Test Cases:

Unavailable?

Applicable | Test Title | Test Summary | Optional or Mandatory | Test Scenario | API Sequence | Expected Result | Actual Result
| ------| ----------- | ----------- | ----- | -------------- | ----------- | ------------- | -------------- |
CRT_ABHA_03 - HRPs / HIPs|ABHA creation - Assisted |Hospital user will create ABHA using patient Aadhaar based mobile OTP|Optional|EMR/HMIS system will take the Aadhaar number, OTP and consent of the patient to create ABHA.|v1/registration/aadhaar/generateOtp, v1/registration/aadhaar/verifyOTP, v1/registration/aadhaar/generateMobileOTP, v1/registration/aadhaar/verifyMobileOTP, v1/registration/aadhaar/createHealthIdbyAadhar, v1/search/existsByHealthId"|Successful creation of ABHA |ABHA generated

## API Sequence 

The sequence of APIs used via this method are shown in the diagram below.


{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
autonumber
actor Client
participant ABHA Server
participant Document Database Server
note left of ABHA Server : Generate OTP on given mobile number
Client->>+ABHA Server: /v3/enrollment/request/otp
ABHA Server-->>-Client: Response: 200 OK 
note right of Client : txnId
Client->>+ABHA Server: /v3/enrollment/enrol/byAadhaar
note left of ABHA Server : OTP, trxnId
ABHA Server-->>-Client: Response: 200 OK 
note right of Client : returns Verified Token
Client->>+ABHA Server: /api/v3/enrollment/enrol/byDocument
ABHA Server->>Document Database Server: Match Document ID with Name, DOB, Gender
Document Database Server-->>ABHA Server: 
ABHA Server-->>-Client: 
note right of Client : Enrollment number 
{{< /mermaid >}}


## API Information Request Response 


**1. [Create Gateway Session Token](/abdm-docs/1-basics/verify_sandbox_access/#create-gateway-session-token)**


**2. Utilities**
- For encrypting the mobile number and otp refer the [link](/abdm-docs/8-utilities/utilities/#rsa-encryption)
- For converting an image into Base64 string refer the [link](/abdm-docs/8-utilities/utilities/#convert-image-to-base64)

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



