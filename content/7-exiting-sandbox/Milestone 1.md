+++
title = " Milestone 1"
date = 2023-03-13T14:30:25+05:30
weight = 5
chapter = true
pre = "<b>7.1</b>"
+++

# Milestone 1

**Milestone 1:** ABHA creation and capture & verification for seamless patient registration

## ABHA APIs Collection

| S.No. | Purpose | Serial | API | Description
| ----------- | ----------- | ----------- | ----------- | ----------- |
1|Registration|1.0.1|v1/auth/cert|Authentication token public certificate. This certificate is also used to encrypt the data.
1.1|Registration Via Aadhaar|1.1.1|v1/registration/aadhaar/generateOtp|Generate Aadhaar OTP on Registered mobile number
||| 1.1.2 |v1/registration/aadhaar/verifyOTP|Verify Aadhaar OTP received on Registered mobile number
|||1.1.3|v1/registration/aadhaar/generateMobileOTP|Generate Mobile OTP for verification.
|||1.1.4|v1/registration/aadhaar/verifyMobileOTP|Verify Mobile OTP in an existing transaction.
|||1.1.5|v1/registration/aadhaar/createHealthIdByAadhar|Create Health ID using pre-verified Aadhaar & Mobile.
|||1.1.6|v1/search/existsByHealthId|Check the ABHA in our system.This API checks ifABHA is reserved/used which includes permanently deleted ABHAs.
1.2|Registration via Mobile|1.2.1|v2/registration/mobile/generateOtp|Generate Mobile OTP to start registration transaction
|||1.2.2|v2/registration/mobile/verifyOtp|Verify Mobile OTP sent as part of registration transaction.
|||1.2.3|v2/registration/mobile/createHidViaMobile|Create ABHA with verified mobile token
|||1.2.4|v2/registration/mobile/resendOtp|Resend Mobile OTP in an existing transaction in case previous OTP is not received.
1.3|Registration via Driving Licence|1.3.1|v2/document/generate/mobile/otp|Generate Mobile OTP
|||1.3.2|v2/document/verify/mobile/otp|Verify Mobile OTP
|||1.3.3|v2/document/validate|Match the provided demographic details against document and check for the already created ABHA or Enrollment number against the document
|||1.3.4|v2/document|Create ABHA using ID documents like Driving Licence
2|Login|2.0.1|v1/auth/cert|Authentication token public certificate. This certificate is also used to encrypt the data.
|||2.0.2|v1/search/searchByHealthId|Check the ABHA in our system.This API checks if ABHA is reserved/used which includes permanently deleted ABHAs.
|||2.0.3|v1/auth/init|Initiate authentication process for given ABHA
2.1|Login via Aadhaar OTP|2.1.1|v1/auth/confirmWithAadhaarOtp|Authentication with Aadhaar OTP based auth transaction
2.2|Login via Mobilr OTP|2.2.1|v1/auth/confirmWithMobileOTP|Authentication with Mobile OTP based auth transaction.
2.3|Login via Password|2.3.1|v1/auth/authPassword|Authenticate using ABHA and password
3|Forgot ABHA|3.0.1|v1/auth/cert|Authentication token public certificate. This certificate is also used to encrypt the data.
|||3.0.2|v1/search/searchByHealthId|Check the ABHA in our system.This API checks if ABHA is reserved/used which includes permanently deleted ABHAs.
3.1|Retrieve ABHA via Aadhaar|3.1.1|v2/auth/reactivate/init|Initiate authentication for reactivation of ABHA
|||3.1.2|v2/auth/reactivate|Confirm reactivation transaction with aadhar or mobile otp
3.2|Retrieve Health ID via Mobile|3.2.1|v2/auth/reactivate/init|Initiate authentication for reactivation of  ABHA
|||3.2.2|v2/auth/reactivate|Confirm reactivation txn with aadhar or mobile otp
3.3|Retrieve Health ID via Password|3.3.1|v2/auth/reactivate/init|Initiate authentication for reactivation of  ABHA
4|Profile|||
4.1|Get Profile|4.1.1|v1/account/profile|Get account information
5|Get QR code|5.1.1|v1/account/qrCode|Get Quick Response code in PNG format for this account.
6|Edit Profile|||
6.1|Update Password|||
6.1.1|Update Password Via Aadhaar Otp|6.1.1.1|v1/account/change/passwd/generateAadhaarOTP|Generate Aadhaar OTP on Registered mobile number.
|||6.1.1.2|v1/account/change/passwd/byAadhaar|Change password via Aadhar for ABHA
|||6.1.1.3|v1/account/logout|Logout
6.1.2|Update Password Via Password|6.1.2.1|v1/account/change/password|Change password via password for ABHA
|||6.1.2.2|v1/account/logout|Logout 
6.1.3|Update Password Via Mobile Otp|6.1.3.1|v1/account/change/passwd/generateMobileOTP|Generate Mobile OTP to start password change process.
|||6.1.3.2|v1/account/change/passwd/byMobile|Change password via mobile for ABHA
|||6.1.3.3|v1/account/logout|Logout
6.2|Update Mobile|||
6.2.1|Update Mobile via Password|6.2.1.1|v2/account/change/mobile/new/generateOTP|Generate OTP on new mobile need to update existing account mobile number
|||6.2.1.2|v2/account/change/mobile/new/verifyOTP |Verify Mobile OTP to complete new mobile update verification.
|||6.2.1.3|v2/account/change/mobile/update/authentication|Change mobile number via password/aadhaar/existing mobile for ABHA
6.2.2|Update Mobile via Aadhaar Otp|6.2.2.1|v2/account/change/mobile/new/generateOTP|Generate OTP on new mobile need to update existing account mobile number
|||6.2.2.2|v2/account/change/mobile/new/verifyOTP |Verify Mobile OTP to complete new mobile update verification.
|||6.2.2.3|v2/account/change/mobile/aadhaar/generateOTP|Generate Aadhaar OTP on Registered mobile number to start mobile update
|||6.2.2.4|v2/account/change/mobile/update/authentication|Change mobile number via password/aadhaar/existing mobile for ABHA
6.2.3|Update Mobile via Mobile Otp|6.2.3.1|v2/account/change/mobile/new/generateOTP|Generate OTP on new mobile need to update existing account mobile number
|||6.2.3.2|v2/account/change/mobile/new/verifyOTP |Verify Mobile OTP to complete new mobile update verification.
|||6.2.3.3|v2/account/change/mobile/old/generateOTP|Generate Mobile OTP to start mobile update.
|||6.2.3.4|v2/account/change/mobile/update/authentication|Change mobile number via password/aadhaar/existing mobile for ABHA
6.3|Update Email|||
6.3.1|Update Email Via Aadhaar Otp|6.3.1.1|v2/account/email/verification/auth/initiate/send|Send the Email Verification Activation Link to verify the E-mail Address
|||6.3.1.2|v2/account/email/verification/auth/verify|Verfiy the user initiate the Activation Link
6.3.2|Update Email Via Mobile Otp|6.3.2.1|v2/account/email/verification/auth/initiate/send|Send the Email Verification Activation Link to verify the E-mail Address
|||6.3.2.2|v2/account/email/verification/auth/verify|Verfiy the user initiate the Activation Link
6.3.3|Update Email Via Password|6.3.3.1|v2/account/email/verification/auth/initiate/send|Send the Email Verification Activation Link to verify the E-mail Address
|||6.3.3.2|v2/account/email/verification/auth/verify|Verfiy the user initiate the Activation Link
||OPT OUT FEATURE|||
7|Delete ABHA|||
7.1|Delete ABHA using Aadhaar|7.1.1|v2/account/aadhaar/generateOTP|Generate Aadhaar OTP on Registered for link account with aadhar number
|||7.1.2|v2/account/profile/delete|Delete account
7.2|Delete ABHA using Mobile |7.2.1|v2/account/mobile/generateOTP|Generate Mobile OTP to start mobile txn.
|||7.2.2|v2/account/profile/delete|Delete account
7.3|Delete ABHA using password|7.3.1|v2/account/profile/delete|Delete account
8|Deactivate ABHA|||
8.1|Deactivate ABHA using Aadhaar|8.1.1|v2/account/aadhaar/generateOTP|Generate Aadhaar OTP on Registered for link account with aadhar number
|||8.1.2|v2/account/profile/deactivate|Deactivate the account using mobile or aadhaar otp.
8.2|Deactivate ABHA using Mobile |8.2.1|v2/account/mobile/generateOTP|Generate Mobile OTP to start mobile txn.
|||8.2.2|v2/account/profile/deactivate|Deactivate the account using mobile or aadhaar otp.
8.3|Deactivate ABHA using password|8.3|v2/account/profile/deactivate|Deactivate the account using mobile or aadhaar otp.

## Test Cases

Test Case#|Applicable To|Test Title|Test Summary|Optional/Mandatory|Test Scenario|API Sequence|Expected Result|Actual Result|Status|Remarks
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
CRT_ABHA_01|HRPs / HIPs|ABHA creation - Modal popup integration|EMR / HMIS system can optionally add a create health id button that links to the ABHA modal pop up portal. On clicking, the ABHA system should open (usually in a new tab/window). If correctly configured, it should ask for the facility's password, allow the user to create a ABHA in assisted mode and then share the ABHA back to the EMR system"|Optional|User clicks on the create ABHA link provided on the Integrators homepage. Clicking on that link will launch the ABHA modal pop up. Verify that details of the ABHA was shared back to the integrators system and the integrator is using it to link to a patient record. |Not Required|Successful registration with Health ID number with QR code on the print slip in the health id portal. And control will again go back to the integrator's solution.|||
CRT_ABHA_02|HRPs / HIPs|ABHA creation - Assisted |Hospital user will create ABHA using patient Aadhaar based mobile OTP|Optional|EMR/HMIS system will take the Aadhaar number| OTP and consent of the patient to create ABHA.|v1/registration/aadhaar/generateOtp, v1/registration/aadhaar/verifyOTP, v1/registration/aadhaar/generateMobileOTP, v1/registration/aadhaar/verifyMobileOTP, v1/registration/aadhaar/createHealthIdbyAadhar, v1/search/existsByHealthId"|Successful creation of ABHA |ABHA generated||
CRT_ABHA_03|EMR/HMIS who implements biometric auth support via APIs|ABHA creation - Assisted using Biometric device|Hospital user will create ABHA using patient Aadhaar through internal system using fingerprint authentication|Optional|EMR/HMIS system will take the Aadhaar number and consent of the patient and authenticate using fingerprint to create health id.|v2/registration/aadhaar/verifyBio, v2/registration/aadhaar/confirm|Successful creation of ABHA with biometric details |||
VRFY_ABHA_01|EMR/HMIS verifying ABHA|ABHA verification during patient registration using ABHA QR code|ABHA verification during patient registration. 1. Health Provider scans the ABHA QR Code shown by the patient in PHR app|Mandatory|EMR/HMIS scans the patients ABHA address QR code to get patient details into his system for registration. - Read contents of ABHA QR code - Does demographic auth to verify the contents (KYC & LINK) - Save linking token|{GATEWAY_HOST}/v0.5/users/auth/fetch-modes, {GATEWAY_HOST}/v0.5/users/auth/init, {GATEWAY_HOST}/v0.5/users/auth/confirm, {GATEWAY_HOST}/v0.5/users/auth/on-notify|EMR/HMIS system will save the ABHA Address as part of its patient's registration. EMR/HMIS system will save the Linking token "|Details are fetched||
VRFY_ABHA_02|EMR/HMIS sharing its facility QR code |Share Patient Profile with HIP by scanning HIP QR code (patient scans the HIP QR code)|Patient scans HIP QR code using their PHR mobile app|Mandatory|-QR code with HIP details is pasted at Health facility Registration desk. -Patients scans the HIP's QR code from PHR app. -Patient's ABHA address is shared with the Integrators system. -EMR/HMIS then does demographic auth to verify the contents (KYC & LINK) and saves linking token|{{CM_HOST}}/providers/{provider-id}, {{CM_HOST}}/patients/profile/share, {GATEWAY_HOST}/v0.5/users/auth/fetch-modes, {GATEWAY_HOST}/v0.5/users/auth/init. {GATEWAY_HOST}/v0.5/users/auth/confirm"|1. EMR/HMIS system will allow the patient to see & select from the list of profiles shared at the counter. 2. EMR/HMIS system will save ABHA Address as part of its patient's registration. 3. EMR/HMIS system will save Linking token |||
VRFY_ABHA_03|EMR/HMIS verifying ABHA|ABHA verification during patient registration using ABHA details shared verbally|ABHA verification during patient registration when patient verbally shares ABHA or ABHA Address|Mandatory|"Patient verbally shares his/her 14 digit ABHA or PHR address (alias to ABHA) and authorization happens through his mobile OTP. -Patient verbally shares Health ID or PHR Address. -Verification through mobile OTP. -Save ABHA address & linking token|/v2/search/searchHealthIdToLogin, /v2/auth/init /v2/auth/confirmWithMobileOtp|1. Check if integrator's system is saving the PHR Address as part of its patient's registration. 2. Check if integrator's system is saving the Linking token|Fetching ABHA||
VRFY_ABHA_ID_04|EMR/HMIS verifying ABHA|ABHA verification during patient registration using ABHA details shared verbally|ABHA verification during patient registration when patient verbally shares ABHA or ABHA Address|Mandatory|Patient verbally shares his/her ABHA or ABHA address and authorization happens through his/her Aadhaar registered mobile OTP. After successful authentication, patient data fields i.e. First Name,Gender,Year of birth, district and state will be populated from health ID. And, successful registration will be done. -Patient verbally shares Health ID or PHR Address. -Verification through mobile OTP. -Save ABHA address & linking token.|/v2/search/searchHealthIdToLogin, /v2/auth/init, /v2/auth/confirmWithAadhaarOtp|SMS will be sent to Aadhaar registered mobile number for verification. After successful authentication, patient record will be displayed on HMIS for registration and further linked to Health ID.|Fetching ABHA||
VRFY_ABHA_ID_05|For returning / existing patients|ABHA address is provided for an existing patient in EMR/HMIS system|System must support saving of ABHA address by all 3 sharing methods (VRFY_HLTH_ID_02 to VRFY_HLTH_ID_04) for existing patients. System must compare demographic information (name, age, gender) and save ABHA address only for same patients|Mandatory|System must support saving of ABHA address by all 3 sharing methods (VRFY_HLTH_ID_02 to VRFY_HLTH_ID_04) for existing patients. System must compare demographic information (name, age, gender) and save ABHA address only for same patients|||||
VRFY_ABHA_ID_06||Health ID verification during patient registration|During ABHA verification all the mandatory fields coming from ABDM should not be editable.|Mandatory|During verification all the mandatory fields coming from ABDM should not be editable and should be locked irrespective of how  the health id was created(mobile/aadhar etc).||All fields should be auto locked.|||
LINK_ABHA_ID_07|HIP|Link Health ID with Episode|HIP should be able to initiate Health ID linking process.PURPOSE: LINK. AUTHMODE: AADHAAR_OTP|Mandatory|HIP should be able to link ABHA with hospital id.|||||
LINK_ABHA_ID_08|HIP|Link Health ID with Episode(Old records)|HIP should be able LINK Health ID for AUTHMODE as DEMOGRAPHICS. PURPOSE: LINK. AUTHMODE: DEMOGRAPHICS|Optional|HIP should be able to link old records. If a patient is registered without ABHA initially then we should be able to link his visit with his ABHA later on.||ABHA will be linked via demographic |||


