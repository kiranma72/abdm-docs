+++
title = "Using Aadhaar OTP"
date = 2023-03-16T09:30:25+05:30
weight = 1
chapter = true
pre = "<b>2.1.1 </b>"
+++

# Registration via Aadhaar OTP

## Functionality Overview 

ABHA Number can be obtained via self-registration using Aadhaar as KYC with valid user consent where user is giving his consent to create ABHA number. **ABHA enrolment using Aadhaar has strong KYC validation.** Once user is successfully authenticated, the system will generate 14 digit ABHA number

Following are the steps to successfully integrate the ABHA registration via Aadhaar:

1. The User should input the Aadhaar number as an input.
2. To enable beneficiary registration using Aadhaar, an integrator needs to generate an OTP and send the same on the linked mobile number.
3. For the OTP verification process there is a primary mobile number which user wants to link with ABHA number.
4. Once the OTP is verified, system should returns the complete profile data along with 14 digit ABHA Number to the user.
5. if the OTP is verified:
    - System checks whether the primary mobile number is matching with Aadhaar linked mobile number. If the aadhaar number matches then it will automatically link with ABHA number.
    - If the primary mobile number is not matching with Aadhaar linked mobile, user must authenticate the mobile number via OTP authentication

**Note:** Mobile Number can be linked/verify with ABHA via using API  

**Sample User experience:**

![sample user experienece](/abdm-docs/img/aadhaar-otp.gif)


## API Sequence 

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
{{< /mermaid >}}


## ABHA OTP Test Cases:

S.No|Functionality|Test Case|Steps To Be Executed|
| -- | ----- | ----- | ----- |
1.1| {{% badge %}}Mandatory{{% /badge %}} Create ABHA Option (CRT_ABHA_101)|The system must provide an option to create ABHA through Aadhaar OTP|
1.2| {{% badge %}}Mandatory{{% /badge %}} Consent collection (CRT_ABHA_102)|The system must display the  consent language/ disclaimer language and collect user's consent as per the ABDM published  consent.|1. Read consent language. 2. Agree to the consent language (through 'I agree' checkbox or any other form of signature)|
|| {{% badge %}}Optional{{% /badge %}} Consent collection should be multilingual  (CRT_ABHA_103)|The system should be able to provide the consent in languages other than English also|1. Read consent language. 2. Agree to the consent language (through 'I agree' checkbox or any other form of signature)|
1.3| {{% badge %}}Mandatory{{% /badge %}} Aadhaar collection and Error Message (CRT_ABHA_104)|System must allow the user to enter Aadhaar Number and the system will display an error message for invalid Aadhaar Number| Enter Aadhaar number|
1.4| {{% badge %}}Mandatory{{% /badge %}} Aadhaar OTP Collection (CRT_ABHA_105)|User receives Aadhaar OTP and System must allow the user to enter Aadhaar OTP|1. Receive OTP on mobile number registered with Aadhaar. 2. Enter Aadhaar OTP|
1.5| {{% badge %}}Mandatory{{% /badge %}} Resend OTP (CRT_ABHA_106)|System may activate the Resend OTP button atleast 2 times after 60 seconds|1. Click on Resend OTP Button. 2. Receive OTP on mobile|
1.6| {{% badge %}}Mandatory{{% /badge %}} OTP based Aadhaar Authentication (CRT_ABHA_107)|System must verify the OTP|Click on verify button(For Resend and Send). It is recommended that verify button be auto enabled|
1.7| {{% badge %}}Optional{{% /badge %}} Communication Mobile Number (CRT_ABHA_108)|1. If communication mobile number is same as Aadhaar linked mobile number then it should directly go to ABHA  creation screen. 2. Alternatively, Integrators may also prompt for OTP  again from the user and then post verification of OTP user can go to ABHA  creation screen.| System will check entered mobile is same as Aadhaar linked mobile number. If returns true then user will directed to ABHA  creation screen.|
1.8| {{% badge %}}Mandatory{{% /badge %}} Mobile Number Verification (CRT_ABHA_109)|If communication mobile number is not same as Aadhaar linked mobile number then system must ask for the OTP to verify comuncation mobile number.|System must verify the mobile number. 1. System must send OTP on mobile number. 2. User enters the OTP and clicks on verify. 3. In case of incorrect OTP| the system displays an error. 4. In case of correct OTP| the system allows the user to proceed|
|| {{% badge %}}Mandatory{{% /badge %}}for Private /Government(Suggested for integrators program using demo auth). Suggested ABHA Address (CRT_ABHA_112)|The system should allow the user to select  the ABHA  address giving atleast 3 available suggestions |1. Governemnt integrator may use the default ABHA  address. 2. System should have a provision for private integrators to proceed with the suggested ABHA  and to create a new ABHA  address.|
1.9| {{% badge %}}Mandatory{{% /badge %}} Display of ABHA Number (CRT_ABHA_113)|System must display the created ABHA Number|1. System shows the 14-digit ABHA number and ABHA  address  generated|
1.10| {{% badge %}}Mandatory{{% /badge %}} for Private. View and Download ABHA details (If integrators is generating ABHA card) (CRT_ABHA_114)|System must have a provision to View / Download ABHA card |1. System should show the user their ABHA Card. 2. ABHA Card should be generated by API and should contain: a. ABHA Number (Mandatory). b. User Photo-Optional. c. ABHA QR code. d. date of birth and gender. e. ABHA Address|
|| {{% badge %}}Mandatory & Optional{{% /badge %}} Either of the test cases CRT_ABHA_114 or CRT_ABHA_115 is mandatory for Governement Optional for Private. View and Download ABHA details. (If integrators  is not  generating ABHA card)  (CRT_ABHA_115)| If Integrator is not generating ABHA card.|1. If Integrator is not generating ABHA card then They print the mentioned information on their own card. a. ABHA Number (Mandatory). b. ABHA Address|


## API Information Request Response 

**1. [Create Gateway Session Token](/abdm-docs/1-basics/verify_sandbox_access/#create-gateway-session-token)**


Bearer token is received as part of respose and should be passed a Authorization token for subsequent API calls.

**BASE URL:** https://dev.ndhm.gov.in/gateway/


**2. Generate Aadhaar OTP on registrered mobile number**

Api accepts Aadhar Card Number and then Generates OTP for Registered Mobile Number

**BASE URL:** https://abhasbx.abdm.gov.in/abha/api

Refer to example “Request OTP Aadhaar based enrollment”

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="POST /v3/enrollment/request/otp$" >}}


**3. Create ABHA Number using pre-verified Aadhaar & Mobile.**

API creates ABHA Number using Aadhaar & Mobile which are already Registered.

**BASE URL:** https://abhasbx.abdm.gov.in/abha/api

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="POST /v3/enrollment/enrol/byAadhaar$" >}}


