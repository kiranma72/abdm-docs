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

ABHA created through Self assisted mode via using Driving license, an 
Enrollment number has been issued which can be verified at any facility centers.
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

**Utilities**
- For encrypting the mobileNumber/AadharNumber/otp refer the [link](/abdm-docs/8-utilities/utilities/#rsa-encryption)

  - To get public key for encrypting:

    **BASE URL:** https://healthidsbx.abdm.gov.in/api

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="GET /v1/auth/cert$" >}}

- For converting an image into Base64 string refer the [link](/abdm-docs/8-utilities/utilities/#convert-image-to-base64)

**1. [Create Gateway Session Token](/abdm-docs/1-basics/verify_sandbox_access/#create-gateway-session-token)**


**2. Request otp to mobile**

Refer to example "Request OTP For DL based enrollment"

**BASE URL:** https://abhasbx.abdm.gov.in/abha/api

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="POST /v3/enrollment/request/otp$" >}}

**3. Verify the mobile**

Refer to example "Request OTP for mobile verfication"

**BASE URL:** https://abhasbx.abdm.gov.in/abha/api

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="POST /v3/enrollment/request/otp$" >}}

**4. Enroll by DL**

**BASE URL:** https://abhasbx.abdm.gov.in/abha/api

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="POST /v3/enrollment/enrol/byDocument" >}}

## Verification and ABHA number creation:
After receiving the enrollment number, the user need to approach any facility centers for creating the ABHA number . Health centers would verify the provided demographic details (Name, DOB, Gender) against the document. They also check for already created ABHA Number or Enrollment number against the document


