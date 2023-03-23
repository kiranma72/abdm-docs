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

Applicable | Test Title | Test Summary | Optional or Mandatory | Test Scenario | API Sequence | Expected Result | Actual Result
| ------| ----------- | ----------- | ----- | -------------- | ----------- | ------------- | -------------- |
CRT_ABHA_02 - HRPs / HIPs|ABHA creation - Assisted |Hospital user will create ABHA using patient Aadhaar based mobile OTP|Optional|EMR/HMIS system will take the Aadhaar number, OTP and consent of the patient to create ABHA.|v1/registration/aadhaar/generateOtp, v1/registration/aadhaar/verifyOTP, v1/registration/aadhaar/generateMobileOTP, v1/registration/aadhaar/verifyMobileOTP, v1/registration/aadhaar/createHealthIdbyAadhar, v1/search/existsByHealthId"|Successful creation of ABHA |ABHA generated

## ABHA OTP Test Cases:

S.No|Function|Applicable To|Mandatory/ Optional|Test Case ID|Functionality|Test Case(to be checked during functional testing)|Steps To Be Executed (By User or Functional Tester)|Expected Result|Status|Remarks|Suggestions for the Functional Tester|
|--|---|---|--|--|----|-----|-----|-----|--|---|-----|
1|||Mandatory|CRT_ABHA_101|Create ABHA Option|The system must provide an option to create ABHA through Aadhaar OTP||User will have an option to create ABHA|||
2|||Mandatory|CRT_ABHA_102|Consent collection|The system must display the  consent language/ disclaimer language and collect user's consent as per the ABDM published  consent.|1. Read consent language. 2. Agree to the consent language (through 'I agree' checkbox or any other form of signature)|User provides consent for sharing of Aadhaar details and creation of ABHA. System records user consent for compliance with Health Data Management Policy.||||

Standard Consent Language for Aadhaar- I, hereby declare that I am voluntarily sharing my Aadhaar Number and demographic information issued by UIDAI, with National Health Authority (NHA) for the sole purpose of creation of ABHA number . I understand that my ABHA number can be used and shared for purposes as may be notified by ABDM from time to time including provision of healthcare services. Further, I am aware that my personal identifiable information (Name, Address, Age, Date of Birth, Gender and Photograph) may be made available to the entities working in the National Digital Health Ecosystem (NDHE) which inter alia includes stakeholders and entities such as healthcare professionals (e.g. doctors), facilities (e.g. hospitals, laboratories) and data fiduciaries (e.g. health programmes), which are registered with or linked to the Ayushman Bharat Digital Mission (ABDM), and various processes there under. I authorize NHA to use my Aadhaar number for performing Aadhaar based authentication with UIDAI as per the provisions of the Aadhaar (Targeted Delivery of Financial and other Subsidies, Benefits and Services) Act 2016 for the aforesaid purpose. I understand that UIDAI will share my e-KYC details, or response of “Yes” with NHA upon successful authentication. I have been duly informed about the option of using other IDs apart from Aadhaar; however, I consciously choose to use Aadhaar number for the purpose of availing benefits across the NDHE. I am aware that my personal identifiable information excluding Aadhaar number / VID number can be used and shared for purposes as mentioned above. I reserve the right to revoke the given consent at any point of time as per provisions of Aadhaar Act and Regulations.

|||Optional |CRT_ABHA_103|"Suggestions:- 
Consent collection should be multilingual "|The system should be able to provide the consent in languages other than English also|"1. Read consent language
2. Agree to the consent language (through 'I agree' checkbox or any other form of signature)"|"User provides consent for sharing of Aadhaar details and creation of ABHA.

System records user consent for compliance with Health Data Management Policy.

"||||||||||||||||||
1.3|||Mandatory|CRT_ABHA_104|Aadhaar collection and Error Message|System must allow the user to enter Aadhaar Number and the system will display an error message for invalid Aadhaar Number|1. Enter Aadhaar number|"User is prompted to enter correct Aadhaar Number

In case user enters an invalid Aadhaar number (A valid Aadhaar is a 12-digit number)| the system shows an error message ""Aadhaar Number is not valid""."||||||||||||||||||
1.4|||Mandatory|CRT_ABHA_105|Aadhaar OTP Collection|User receives Aadhaar OTP and System must allow the user to enter Aadhaar OTP|"1. Receive OTP on mobile number registered with Aadhaar
2. Enter Aadhaar OTP"|User will be able to enter a valid Aadhaar OTP (A valid Aadhaar OTP is a 6-digit number)|||"API Sequence -
/v1/registration/aadhaar/generateOtp"|||||||||||||||
1.5|||Mandatory|CRT_ABHA_106|Resend OTP|System may activate the Resend OTP button atleast 2 times after 60 seconds|"1. Click on Resend OTP Button
2. Receive OTP on mobile"|User will able to send OTP again and verify it|||"API - 
/v1/registration/aadhaar/resendAadhaarOtp"|||||||||||||||
1.6|||Mandatory|CRT_ABHA_107|OTP based Aadhaar Authentication|System must verify the OTP|"Click on verify button  (For Resend and Send)

It is recommended that verify button be auto enabled"|"System authenticates the user's Aadhaar through OTP

In case of incorrect OTP| the system displays an error
In case of correct OTP| the system allows the user to proceed"|||"API - 
/v1/registration/aadhaar/verifyOTP"|||||||||||||||
1.7|||Optional|CRT_ABHA_108|Communication Mobile Number|"1. If communication mobile number is same as Aadhaar linked mobile number then it should directly go to ABHA  creation screen .

2. Alternatively | Integrators may also prompt for OTP  again from the user and then post verification of OTP user can go to ABHA  creation screen."|" This is applicable for testcase cell no -G20 | point no-1 

System will check entered mobile is same as Aadhaar linked mobile number. If returns true then user will directed to ABHA  creation screen.


2. For point number 2 step are already mentioned in test case cell no- G20 | point no-2 


"|Redirect to the ABHA  creation screen.||||||||||||||||||
1.8|||Mandatory|CRT_ABHA_109|Mobile Number Verification|If communication mobile number is not same as Aadhaar linked mobile number then system must ask for the OTP to verify comuncation mobile number.|"1. System must verify the mobile number.
1. System must send OTP on mobile number 
2. User enters the OTP and clicks on verify
3. In case of incorrect OTP| the system displays an error
4. In case of correct OTP| the system allows the user to proceed"|System verifies the communication mobile number|||"API for mobile verification - 
/v2/registration/aadhaar/checkAndGenerateMobileOTP

API for mobile OTP verification - 
/v1/registration/aadhaar/verifyMobileOTP"|||||||||||||||
|||Mandatory for Private /Government(Suggested for integrators program using demo auth)|CRT_ABHA_112|Suggested ABHA Address|The system should allow the user to select  the ABHA  address giving atleast 3 available suggestions |"1. Governemnt integrator may use the default ABHA  address.
2. System should have a provision for private integrators to proceed with the suggested ABHA  and to create a new ABHA  address."|User should able to proceed with the ABHA  Address.||||||||||||||||||
1.11|||Mandatory|CRT_ABHA_113|Display of ABHA Number|System must display the created ABHA Number|"1. System shows the 14-digit ABHA number and ABHA  address  generated
"|User should be able to view the generated ABHA Number|||"API - 
/v1/registration/aadhaar/createHealthIdWithPreVerified"|||||||||||||||
1.12|||Mandatory for Private |CRT_ABHA_114|"View and Download ABHA details. 
(If integrators is generating ABHA card) "|System must have a provision to View / Download ABHA card |"1. System should show the user their ABHA Card
2. ABHA Card should be generated by API and should contain -
a. ABHA Number (Mandatory)
b. User Photo-Optional
c. ABHA QR code
d. date of birth and gender
e. ABHA Address"|User should be able to view their ABHA Card|||"API - 
/v1/account/getCard
OR 
/v1/account/getPngCard"|||||||||||||||
|||"Either of the test cases CRT_ABHA_114 or CRT_ABHA_115 is mandatory for Governement 


Optional for Private "|CRT_ABHA_115|"View and Download ABHA details. 
(If integrators  is not  generating ABHA card) "| If Integrator is not generating ABHA card.|"1. If Integrator is not generating ABHA card then They print the mentioned information on their own card.
a. ABHA Number (Mandatory)
b. ABHA Address"|User should be able to view card with ABHA  number and ABHA  address.||||||||||||||||||


## API Information Request Response 

**1. [Create Gateway Session Token](/abdm-docs/1-basics/verify_sandbox_access/#create-gateway-session-token)**


Bearer token is received as part of respose and should be passed a Authorization token for subsequent API calls.

**URL:** https://dev.ndhm.gov.in/gateway/v0.5/sessions


**2. Generate Aadhaar OTP on registrered mobile number**

Api accepts Aadhar Card Number and then Generates OTP for Registered Mobile Number

**URL:** https://abhasbx.abdm.gov.in/abha/api/v3/enrollment/request/otp

Refer to example “Request OTP Aadhaar based enrollment”

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="POST /v3/enrollment/request/otp$" >}}



**3. Create ABHA Number using pre-verified Aadhaar & Mobile.**

API creates ABHA Number using Aadhaar & Mobile which are already Registered.

**URL:** https://abhasbx.abdm.gov.in/abha/api/v3/enrollment/enrol/byAadhaar

{{< swaggermin src="/abdm-docs/Yaml/abha_enrollment_api.yml" api="POST /v3/enrollment/enrol/byAadhaar$" >}}


