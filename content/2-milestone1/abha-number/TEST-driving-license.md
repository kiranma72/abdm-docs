+++
title = "ACTUAL Using Driving Licence"
date = 2023-03-16T09:30:25+05:30
weight = 4.5
chapter = true
pre = "<b>2.1.4 </b>"
+++


# ABHA Number Creation via Driving Licence

|  Applicable To                             |   HMIS / LMIS (PVT)  |   Government Health App  |  
|-------------------------------|:----------------------:|:--------------------:|
|   Using Driving License                     |  {{% badge %}}Optional{{% /badge %}}       |  {{% badge %}}Optional{{% /badge %}}         |  


## Functionality Overview

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

## Test Cases:

The following test cases are applicable to All the stakeholders.

S.No.|Functionality|Test Case|Steps To Be Executed|
|--|----- | ----- | ----- |
1|{{% badge %}}Optional{{% /badge %}} Create ABHA Option (CRT_ABHA_401)|The system must provide an option to create ABHA through Driving License / PAN||
2|{{% badge %}}Optional{{% /badge %}} Consent collection (CRT_ABHA_402)| The system must display the  consent language/ disclaimer language and collect user's consent as per the ABDM published  consent.|1. Read consent language. 2. Agree to the consent language (through 'I agree' checkbox or any other form of signature)|
3|{{% badge %}}Optional{{% /badge %}} Consent collection should be multilingual  (CRT_ABHA_403)|The system should be able to provide the consent in languages other than English also|1. Read consent language. 2. Agree to the consent language (through 'I agree' checkbox or any other form of signature)|
4|{{% badge %}}Optional{{% /badge %}} Communication Mobile Number (CRT_ABHA_404)|1. If communication mobile number is same as Aadhaar linked mobile number then it should directly go to ABHA creation screen. 2. Alternatively, Integrators may also prompt for OTP  again from the user and then post verification of OTP user can go to ABHA  creation screen.|System will check entered mobile is same as Aadhaar linked mobile number. If returns true then user will directed to ABHA  creation screen.|
5|{{% badge %}}Optional{{% /badge %}} Mobile Number Verification (CRT_ABHA_405)|If communication mobile number is not same as Aadhaar linked mobile number then system must ask for the OTP to verify comuncation mobile number.|System must verify the mobile number. 1. System must send OTP on mobile number. 2. User enters the OTP and clicks on verify. 3. In case of incorrect OTP| the system displays an error. 4. In case of correct OTP, the system allows the user to proceed.|
6|{{% badge %}}Optional{{% /badge %}} Document Verification (CRT_ABHA_406)|System must verify the provided document - Driving License / PAN|Enter the Driving License / PAN number. 2. Enter name, date of birth and gender as per the document|
7|{{% badge %}}Optional{{% /badge %}} Document Upload (CRT_ABHA_407)|System must allow upload of front and back page of the Driving licence/ PAN|Upload the front and back page of the document i.e Driving License / PAN.|
8|{{% badge %}}Optional{{% /badge %}} Manual Verification and ABHA Creation (CRT_ABHA_408)|System Operator / healthcare worker must manually check the documents - Driving License / PAN|A healthcare worker/ system operator manually verifies the Driving License / PAN|
9|{{% badge %}}Optional{{% /badge %}} Display of ABHA Number (CRT_ABHA_409)|System must display the created ABHA Number|1. System shows the 14-digit ABHA number and ABHA  address  generated. 2. The Label should read  ABHA Number and not  Health ID|
10|{{% badge %}}Optional{{% /badge %}} View and Download ABHA details. (If integrators is generating ABHA card)  (CRT_ABHA_410)|System must have a provision to View / Download ABHA card |1. System should show the user their ABHA Card. 2. ABHA Card should be generated by API and should contain - ABHA Number (Mandatory), User Photo-Optional, ABHA QR code, date of birth and gender, ABHA Address|
11|{{% badge %}}Optional{{% /badge %}} View and Download ABHA details.(If integrators  is not  generating ABHA card)  (CRT_ABHA_411)"| If Integrator is not generating ABHA card.|If Integrator is not generating ABHA card then They print the mentioned information on their own card: ABHA Number (Mandatory), ABHA Address|


## API Sequence 

The sequence of APIs used via this method are shown in the diagram below:

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Notification on Consent Grant
actor Client
Note right of Client: Generate OTP on given Mobile Number
Client->>ABHA Server:v3/enrollment/request/otp
activate ABHA Server
ABHA Server-->> Client: Response 200 OK
deactivate ABHA Server
Note right of Client: Txn Id
Client->>ABHA Server:v3/enrol/byAadhaar
activate ABHA Server
Note left of ABHA Server: OTP, Txn Id
ABHA Server-->> Client: Response 200 OK
Note right of Client: Returns verified Token
deactivate ABHA Server
Client->>ABHA Server:v3/enrol/byDocument
activate ABHA Server
ABHA Server->> Document Database Server: Match Document ID with Name, Gender & DOB
deactivate ABHA Server
ABHA Server-->> Client: 
Note right of Client: Enrollment number
{{< /mermaid >}}


## API Information Request Response 

**Utilities**
- For encrypting the mobileNumber/AadharNumber/otp refer the [link](/abdm-docs/8-utilities/utilities/#rsa-encryption)

  - To get public key for encrypting refer the [link](/abdm-docs/8-utilities/utilities/#api-to-retrieve-the-public-key)

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
After receiving the enrollment number, the user need to approach any facility centers for creating the ABHA number .
![facility_center_link](../facility_center_link.png)
![search_facility](../search_facility.png)

 Health centers would verify the provided demographic details (Name, DOB, Gender) against the document. They also check for already created ABHA Number or Enrollment number against the document


