+++
title = "Using Aadhaar OTP"
date = 2023-03-16T09:30:25+05:30
weight = 1
chapter = true
pre = "<b>2.1.1 </b>"
+++

# Registration via Aadhaar OTP


|  Applicable To                             |   HMIS / LMIS (PVT)  |   Government Health App  |  
|-------------------------------|:----------------------:|:--------------------:|
|   Using Aadhar OTP                      |  {{% badge style="blue" %}}Mandatory{{% /badge %}}       |  {{% badge style="blue" %}} Mandatory{{% /badge %}}        |  


## Functionality Overview 

ABHA Number can be created by authenticating with Aadhaar. Those who have their Aadhaar number linked with their mobile number can use this method to generate their ABHA no. Consent must be explained & collected from the user prior to performing AAdhaar OTP authentication.  Once user is successfully authenticated, the system will generate 14 digit ABHA number. 

Following are the steps to create a ABHA Number via Aadhaar OTP authentication:

1. The User should input their Aadhaar number.
2. The ABHA number APIs will make a request to UIDAI to send an OTP to the aadhaar linked mobile number. 
3. Once the OTP is verified, the system returns the complete profile data along with 14 digit ABHA Number.
4. The User is asked to input their mobile number.   
    - System checks whether the user's mobile number is matching with Aadhaar linked mobile number. If it matches then it will automatically link with ABHA number.
    - If the mobile number is not matching with Aadhaar linked mobile, an OTP is triggered to verify the submitted the mobile number


## Sample User experience

![sample user experienece](/abdm-docs/img/aadhaar-otp.gif)

## ABHA OTP Test Cases

S.No|Functionality|Test Case|Steps To Be Executed|
| -- | ----- | ----- | ----- |
1.1| {{% badge style="blue" %}}Mandatory{{% /badge %}} Create ABHA Option (CRT_ABHA_101)|The system must provide an option to create ABHA through Aadhaar OTP|
1.2| {{% badge style="blue" %}}Mandatory{{% /badge %}} Consent collection (CRT_ABHA_102)|The system must display the  consent language/ disclaimer language and collect user's consent as per the ABDM published  consent.|1. Read consent language. 2. Agree to the consent language (through 'I agree' checkbox or any other form of signature)|
|| {{% badge %}}Optional{{% /badge %}} Consent collection should be multilingual  (CRT_ABHA_103)|The system should be able to provide the consent in languages other than English also|1. Read consent language. 2. Agree to the consent language (through 'I agree' checkbox or any other form of signature)|
1.3| {{% badge style="blue" %}}Mandatory{{% /badge %}} Aadhaar collection and Error Message (CRT_ABHA_104)|System must allow the user to enter Aadhaar Number and the system will display an error message for invalid Aadhaar Number| Enter Aadhaar number|
1.4| {{% badge style="blue" %}}Mandatory{{% /badge %}} Aadhaar OTP Collection (CRT_ABHA_105)|User receives Aadhaar OTP and System must allow the user to enter Aadhaar OTP|1. Receive OTP on mobile number registered with Aadhaar. 2. Enter Aadhaar OTP|
1.5| {{% badge style="blue" %}}Mandatory{{% /badge %}} Resend OTP (CRT_ABHA_106)|System may activate the Resend OTP button atleast 2 times after 60 seconds|1. Click on Resend OTP Button. 2. Receive OTP on mobile|
1.6| {{% badge style="blue" %}}Mandatory{{% /badge %}} OTP based Aadhaar Authentication (CRT_ABHA_107)|System must verify the OTP|Click on verify button(For Resend and Send). It is recommended that verify button be auto enabled|
1.7| {{% badge %}}Optional{{% /badge %}} Communication Mobile Number (CRT_ABHA_108)|1. If communication mobile number is same as Aadhaar linked mobile number then it should directly go to ABHA  creation screen. 2. Alternatively, Integrators may also prompt for OTP  again from the user and then post verification of OTP user can go to ABHA  creation screen.| System will check entered mobile is same as Aadhaar linked mobile number. If returns true then user will directed to ABHA  creation screen.|
1.8| {{% badge style="blue" %}}Mandatory{{% /badge %}} Mobile Number Verification (CRT_ABHA_109)|If communication mobile number is not same as Aadhaar linked mobile number then system must ask for the OTP to verify comuncation mobile number.|System must verify the mobile number. 1. System must send OTP on mobile number. 2. User enters the OTP and clicks on verify. 3. In case of incorrect OTP| the system displays an error. 4. In case of correct OTP| the system allows the user to proceed|
|| {{% badge style="blue" %}}Mandatory{{% /badge %}}for Private /Government(Suggested for integrators program using demo auth). Suggested ABHA Address (CRT_ABHA_112)|The system should allow the user to select  the ABHA  address giving atleast 3 available suggestions |1. Governemnt integrator may use the default ABHA  address. 2. System should have a provision for private integrators to proceed with the suggested ABHA  and to create a new ABHA  address.|
1.9| {{% badge style="blue" %}}Mandatory{{% /badge %}} Display of ABHA Number (CRT_ABHA_113)|System must display the created ABHA Number|1. System shows the 14-digit ABHA number and ABHA  address  generated|
1.10| {{% badge style="blue" %}}Mandatory{{% /badge %}} for Private. View and Download ABHA details (If integrators is generating ABHA card) (CRT_ABHA_114)|System must have a provision to View / Download ABHA card |1. System should show the user their ABHA Card. 2. ABHA Card should be generated by API and should contain: a. ABHA Number (Mandatory). b. User Photo-Optional. c. ABHA QR code. d. date of birth and gender. e. ABHA Address|
|| {{% badge style="blue" %}}Mandatory & Optional{{% /badge %}} Either of the test cases CRT_ABHA_114 or CRT_ABHA_115 is mandatory for Governement Optional for Private. View and Download ABHA details. (If integrators  is not  generating ABHA card)  (CRT_ABHA_115)| If Integrator is not generating ABHA card.|1. If Integrator is not generating ABHA card then They print the mentioned information on their own card. a. ABHA Number (Mandatory). b. ABHA Address|




## API Information Request Response 

{{%notice%}}
**Utilities**
- [To encrypt the mobileNumber/AadharNumber/otp](/abdm-docs/1-basics/encoding-rsa-encryption/#rsa-encryption)
- [To get public key for encryption](/abdm-docs/1-basics/encoding-rsa-encryption/#api-to-retrieve-the-public-key)
- [To convert an image into Base64 string](/abdm-docs/1-basics/encoding-rsa-encryption/#convert-image-to-base64)
- [Use the Postman Collection to try out the APIs](/abdm-docs/1-basics/postman_setup/#download-collections-and-environment-variables)
- [To obtain Gateway Session Token](/abdm-docs/1-basics/verify_sandbox_access/#create-gateway-session-token)
{{%/notice%}}

{{% notice title="API Versions" %}}

- **V1&V2 API**
  - [Sequence Diagram for V1&V2 API](#sequence-diagram-for-v1v2-api)
  - [API Information Request Response for V1&V2](#api-information-request-response-for-v1v2)
- **V3 API**
  - [Sequence Diagram for V3 API](#sequence-diagram-for-v3-api)
  - [API Information Request Response for V3](#api-information-request-response-for-v3)

{{% /notice %}}

## Sequence Diagram for V1&V2 API

#### Mobile Number Linked With Aadhaar Flow

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title ABHA Creation using Aadhar OTP
actor User
participant HIU/HIP/PHR
Note left of ABHA: Share RSA Encrypted Aadhaar number
HIU/HIP/PHR->>ABHA: (POST: /v2/registration/aadhaar/generateOtp)
ABHA->>UIDAI: Aadhaar number
UIDAI->>UIDAI:Verify Aadhaar number
UIDAI->>ABHA: Response 200
ABHA->>HIU/HIP/PHR: Response 200 (transaction ID, last 4 digit mobile number)
UIDAI->>User: OTP
Note right of HIU/HIP/PHR:Receive OTP
Note left of ABHA: Share OTP, transaction ID
HIU/HIP/PHR->>ABHA: (POST: /v2/registration/aadhaar/verifyOTP)
ABHA->>UIDAI: 
UIDAI->>UIDAI:Verify OTP
UIDAI->>ABHA: 
ABHA->>HIU/HIP/PHR: Response 200 (user details,transaction ID)
Note left of ABHA: Share mobile number, transaction ID
HIU/HIP/PHR->>ABHA: (POST: /v2/registration/aadhaar/checkAndGenerateMobileOTP)
ABHA->>HIU/HIP/PHR: Response 200 (mobileLinked,transaction ID)
Note over HIU/HIP/PHR,UIDAI: mobileLinked : true (mobile number linked with Aadhaar)
Note left of ABHA: transaction ID
HIU/HIP/PHR->>ABHA: (POST: /v2/registration/aadhaar/createHealthIdByAdhaar)
Note right of HIU/HIP/PHR: ABHA number created
ABHA->>HIU/HIP/PHR: Response 200 (user account details)
{{< /mermaid >}}

#### Mobile Number Not Linked With Aadhaar Flow

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title ABHA Creation using Aadhar OTP
actor User
participant HIU/HIP/PHR
Note left of ABHA: Share RSA Encrypted Aadhaar number
HIU/HIP/PHR->>ABHA: (POST: /v2/registration/aadhaar/generateOtp)
ABHA->>UIDAI: Aadhaar number
UIDAI->>UIDAI:Verify Aadhaar number
UIDAI->>ABHA: Response 200
ABHA->>HIU/HIP/PHR: Response 200 (transaction ID, last 4 digit mobile number)
UIDAI->>User: OTP
Note right of HIU/HIP/PHR:Receive OTP
Note left of ABHA: Share OTP, transaction ID
HIU/HIP/PHR->>ABHA: (POST: /v2/registration/aadhaar/verifyOTP)
ABHA->>UIDAI: 
UIDAI->>UIDAI:Verify OTP
UIDAI->>ABHA: 
ABHA->>HIU/HIP/PHR: Response 200 (user details,transaction ID)
Note left of ABHA: Share mobile number, transaction ID
HIU/HIP/PHR->>ABHA: (POST: /v2/registration/aadhaar/checkAndGenerateMobileOTP)
ABHA->>HIU/HIP/PHR: Response 200 (mobileLinked,transaction ID)
Note over HIU/HIP/PHR,UIDAI: mobileLinked : false (mobile number not linked with Aadhaar)
Note right of HIU/HIP/PHR: sends OTP
ABHA->>User: OTP
Note left of ABHA: Share OTP, transaction ID
HIU/HIP/PHR->>ABHA: (POST: /v2/registration/aadhaar/verifyMobileOTP)
ABHA->>HIU/HIP/PHR: Response 200 (transaction ID)
Note left of ABHA: Share transaction ID
HIU/HIP/PHR->>ABHA: (POST: /v2/registration/aadhaar/createHealthIdByAdhaar)
ABHA->>HIU/HIP/PHR:  ABHA number created
{{< /mermaid >}}

## API Information Request Response for V1&V2

**1. Generate OTP On Aadhaar Registered Mobile**

**BASE URL:** https://healthidsbx.abdm.gov.in

BasePath : api

{{< swaggermin src="/abdm-docs/Yaml/hidsbx.yml" api="POST /{BasePath}/v2/registration/aadhaar/generateOtp$" >}}

**2. Verify OTP**

**BASE URL:** https://healthidsbx.abdm.gov.in

BasePath : api

{{< swaggermin src="/abdm-docs/Yaml/hidsbx.yml" api="POST /{BasePath}/v2/registration/aadhaar/verifyOTP$" >}}

**3. Check Aadhaar Linked Mobile**

**BASE URL:** https://healthidsbx.abdm.gov.in

BasePath : api

{{< swaggermin src="/abdm-docs/Yaml/hidsbx.yml" api="POST /{BasePath}/v2/registration/aadhaar/checkAndGenerateMobileOTP$" >}}

**4. Verify OTP**

**BASE URL:** https://healthidsbx.abdm.gov.in

BasePath : api

{{< swaggermin src="/abdm-docs/Yaml/hidsbx.yml" api="POST /{BasePath}/v2/registration/aadhaar/verifyMobileOTP$" >}}

**Note:** This step is required only if the mobile number is different from the Aadhaar linked mobile number


**5. Create ABHA Number**

**BASE URL:** https://healthidsbx.abdm.gov.in

BasePath : api

{{< swaggermin src="/abdm-docs/Yaml/hidsbx.yml" api="POST /{BasePath}/v2/registration/aadhaar/createHealthIdByAdhaar$" >}}


## Sequence Diagram for V3 API


The sequence of APIs used via this method are shown in the diagram below:

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title ABHA Creation using Aadhar OTP
actor HIU/HIP/PHR
Note left of ABHA: Share encrypted Aadhaar number
HIU/HIP/PHR->>ABHA: (POST: /v3/enrollment/request/otp)
ABHA->>UIDAI: Aadhaar number
UIDAI->>UIDAI:Verify Aadhaar number
UIDAI->>ABHA: Response 200
ABHA->>HIU/HIP/PHR: Response 200 (transaction ID)
UIDAI->>HIU/HIP/PHR:Receive OTP
Note right of HIU/HIP/PHR: Forward OTP & transaction ID to verify
HIU/HIP/PHR->>ABHA: (POST: /v3/enrollment/enrol/byAadhaar)
ABHA->>UIDAI: Forward OTP
UIDAI->>UIDAI: Verify OTP
UIDAI->>ABHA: Share Aadhaar e-KYC details
ABHA->>ABHA: ABHA Creation
ABHA->>HIU/HIP/PHR: ABHA Number & Profile
Note over HIU/HIP/PHR,UIDAI: Mobile verification and Mobile Update
Note left of ABHA: Share encrypted mobile number,transaction ID
HIU/HIP/PHR->>ABHA: (POST: /v3/enrollment/request/otp)
ABHA->>HIU/HIP/PHR: Response 200 
ABHA->>HIU/HIP/PHR:Receive OTP
Note right of HIU/HIP/PHR: Forward Encrypted OTP & transaction ID to verify
HIU/HIP/PHR->>ABHA: (POST: /v3/enrollment/auth/byAbdm)
ABHA->>ABHA: OTP Verified & Mobile Number Linked
ABHA->>HIU/HIP/PHR: Response 200
{{< /mermaid >}}


## API Information Request Response for V3

**BASE URL:** https://dev.ndhm.gov.in/gateway/


**1. Generate Aadhaar OTP on registrered mobile number**

Api accepts Aadhaar Number and then sends OTP to Aadhaar linked mobile number

**BASE URL:** https://abhasbx.abdm.gov.in/abha/api

Refer to example “Request OTP Aadhaar based enrollment”

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="POST /v3/enrollment/request/otp$" >}}

{{% badge style="note" title=" "%}}Note{{% /badge %}} System may activate the Resend OTP button atleast 2 times after 60 seconds. The above api is also used for **Resend OTP**


**2. Create ABHA Number using pre-verified Aadhaar & Mobile.**

API creates ABHA Number using Aadhaar & Mobile which are already Registered.

**BASE URL:** https://abhasbx.abdm.gov.in/abha/api

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="POST /v3/enrollment/enrol/byAadhaar$" >}}

**Verify & Update Mobile**
This step is required only if the mobile number is different from the Aadhaar linked mobile number

**3. Generate OTP on mobile number**

Api accepts Encrypted Mobile Number and then Generates OTP to that Mobile Number

**BASE URL:** https://abhasbx.abdm.gov.in/abha/api

Refer to example “Request OTP for mobile verification”

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="POST /v3/enrollment/request/otp$" >}}

**4. Link mobile number**

Api accepts Encrypted OTP and then link that Mobile Number

**BASE URL:** https://abhasbx.abdm.gov.in/abha/api

Refer to example “Request Verify Mobile”

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="POST /v3/enrollment/auth/byAbdm$" >}}


