+++
title = " Milestone 1 - Test Cases"
date = 2023-03-13T14:30:25+05:30
weight = 5
chapter = true
pre = "<b>7.1</b>"
+++

# Milestone 1 - Test Cases

Milestone 1: ABHA creation and capture & verification for seamless patient registration

| S.No. | Purpose | Serial | API | Description
| ----------- | ----------- | ----------- | ----------- | ----------- |
1|Registration|1.0.1|v1/auth/cert|Authentication token public certificate. This certificate is also used to encrypt the data.
||||
1.1|Registration Via Aadhaar|1.1.1|v1/registration/aadhaar/generateOtp|Generate Aadhaar OTP on Registered mobile number
||| 1.1.2 |v1/registration/aadhaar/verifyOTP|Verify Aadhaar OTP received on Registered mobile number
|||1.1.3|v1/registration/aadhaar/generateMobileOTP|Generate Mobile OTP for verification.
|||1.1.4|v1/registration/aadhaar/verifyMobileOTP|Verify Mobile OTP in an existing transaction.
|||1.1.5|v1/registration/aadhaar/createHealthIdByAadhar|Create Health ID using pre-verified Aadhaar & Mobile.
|||1.1.6|v1/search/existsByHealthId|Check the ABHA in our system.This API checks ifABHA is reserved/used which includes permanently deleted ABHAs.
||||
1.2|Registration via Mobile|1.2.1|v2/registration/mobile/generateOtp|Generate Mobile OTP to start registration transaction
|||1.2.2|v2/registration/mobile/verifyOtp|Verify Mobile OTP sent as part of registration transaction.
|||1.2.3|v2/registration/mobile/createHidViaMobile|Create ABHA with verified mobile token
|||1.2.4|v2/registration/mobile/resendOtp|Resend Mobile OTP in an existing transaction in case previous OTP is not received.
||||
1.3|Registration via Driving Licence|1.3.1|v2/document/generate/mobile/otp|Generate Mobile OTP
|||1.3.2|v2/document/verify/mobile/otp|Verify Mobile OTP
|||1.3.3|v2/document/validate|Match the provided demographic details against document and check for the already created ABHA or Enrollment number against the document
|||1.3.4|v2/document|Create ABHA using ID documents like Driving Licence
||||
2|Login|2.0.1|v1/auth/cert|Authentication token public certificate. This certificate is also used to encrypt the data.
|||2.0.2|v1/search/searchByHealthId|Check the ABHA in our system.This API checks if ABHA is reserved/used which includes permanently deleted ABHAs.
|||2.0.3|v1/auth/init|Initiate authentication process for given ABHA
||||
2.1|Login via Aadhaar OTP|2.1.1|v1/auth/confirmWithAadhaarOtp|Authentication with Aadhaar OTP based auth transaction
||||
2.2|Login via Mobilr OTP|2.2.1|v1/auth/confirmWithMobileOTP|Authentication with Mobile OTP based auth transaction.
||||
2.3|Login via Password|2.3.1|v1/auth/authPassword|Authenticate using ABHA and password
||||
3|Forgot ABHA|3.0.1|v1/auth/cert|Authentication token public certificate. This certificate is also used to encrypt the data.
|||3.0.2|v1/search/searchByHealthId|Check the ABHA in our system.This API checks if ABHA is reserved/used which includes permanently deleted ABHAs.
||||
3.1|Retrieve ABHA via Aadhaar|3.1.1|v2/auth/reactivate/init|Initiate authentication for reactivation of ABHA
|||3.1.2|v2/auth/reactivate|Confirm reactivation transaction with aadhar or mobile otp
||||
3.2|Retrieve Health ID via Mobile|3.2.1|v2/auth/reactivate/init|Initiate authentication for reactivation of  ABHA
|||3.2.2|v2/auth/reactivate|Confirm reactivation txn with aadhar or mobile otp
||||
3.3|Retrieve Health ID via Password|3.3.1|v2/auth/reactivate/init|Initiate authentication for reactivation of  ABHA
||||
4|Profile|||
4.1|Get Profile|4.1.1|v1/account/profile|Get account information
||||
5|Get QR code|5.1.1|v1/account/qrCode|Get Quick Response code in PNG format for this account.
||||
6|Edit Profile|||
||||
6.1|Update Password|||
6.1.1|Update Password Via Aadhaar Otp|6.1.1.1|v1/account/change/passwd/generateAadhaarOTP|Generate Aadhaar OTP on Registered mobile number.
|||6.1.1.2|v1/account/change/passwd/byAadhaar|Change password via Aadhar for ABHA
|||6.1.1.3|v1/account/logout|Logout
||||
6.1.2|Update Password Via Password|6.1.2.1|v1/account/change/password|Change password via password for ABHA
|||6.1.2.2|v1/account/logout|Logout 
||||
6.1.3|Update Password Via Mobile Otp|6.1.3.1|v1/account/change/passwd/generateMobileOTP|Generate Mobile OTP to start password change process.
|||6.1.3.2|v1/account/change/passwd/byMobile|Change password via mobile for ABHA
|||6.1.3.3|v1/account/logout|Logout
||||
6.2|Update Mobile|||
6.2.1|Update Mobile via Password|6.2.1.1|v2/account/change/mobile/new/generateOTP|Generate OTP on new mobile need to update existing account mobile number
|||6.2.1.2|v2/account/change/mobile/new/verifyOTP |Verify Mobile OTP to complete new mobile update verification.
|||6.2.1.3|v2/account/change/mobile/update/authentication|Change mobile number via password/aadhaar/existing mobile for ABHA
||||
6.2.2|Update Mobile via Aadhaar Otp|6.2.2.1|v2/account/change/mobile/new/generateOTP|Generate OTP on new mobile need to update existing account mobile number
|||6.2.2.2|v2/account/change/mobile/new/verifyOTP |Verify Mobile OTP to complete new mobile update verification.
|||6.2.2.3|v2/account/change/mobile/aadhaar/generateOTP|Generate Aadhaar OTP on Registered mobile number to start mobile update
|||6.2.2.4|v2/account/change/mobile/update/authentication|Change mobile number via password/aadhaar/existing mobile for ABHA
||||
6.2.3|Update Mobile via Mobile Otp|6.2.3.1|v2/account/change/mobile/new/generateOTP|Generate OTP on new mobile need to update existing account mobile number
|||6.2.3.2|v2/account/change/mobile/new/verifyOTP |Verify Mobile OTP to complete new mobile update verification.
|||6.2.3.3|v2/account/change/mobile/old/generateOTP|Generate Mobile OTP to start mobile update.
|||6.2.3.4|v2/account/change/mobile/update/authentication|Change mobile number via password/aadhaar/existing mobile for ABHA
||||
6.3|Update Email|||
6.3.1|Update Email Via Aadhaar Otp|6.3.1.1|v2/account/email/verification/auth/initiate/send|Send the Email Verification Activation Link to verify the E-mail Address
||6.3.1.2|v2/account/email/verification/auth/verify|Verfiy the user initiate the Activation Link
||||
6.3.2|Update Email Via Mobile Otp|6.3.2.1|v2/account/email/verification/auth/initiate/send|Send the Email Verification Activation Link to verify the E-mail Address
|||6.3.2.2|v2/account/email/verification/auth/verify|Verfiy the user initiate the Activation Link
||||
6.3.3|Update Email Via Password|6.3.3.1|v2/account/email/verification/auth/initiate/send|Send the Email Verification Activation Link to verify the E-mail Address
|||6.3.3.2|v2/account/email/verification/auth/verify|Verfiy the user initiate the Activation Link
||||
|OPT OUT FEATURE|||
7|Delete ABHA|||
7.1|Delete ABHA using Aadhaar|7.1.1|v2/account/aadhaar/generateOTP|Generate Aadhaar OTP on Registered for link account with aadhar number
||7.1.2|v2/account/profile/delete|Delete account
||||
7.2|Delete ABHA using Mobile |7.2.1|v2/account/mobile/generateOTP|Generate Mobile OTP to start mobile txn.
|||7.2.2|v2/account/profile/delete|Delete account
||||
7.3|Delete ABHA using password|7.3.1|v2/account/profile/delete|Delete account
||||
8|Deactivate ABHA|||
8.1|Deactivate ABHA using Aadhaar|8.1.1|v2/account/aadhaar/generateOTP|Generate Aadhaar OTP on Registered for link account with aadhar number
|||8.1.2|v2/account/profile/deactivate|Deactivate the account using mobile or aadhaar otp.
||||
8.2|Deactivate ABHA using Mobile |8.2.1|v2/account/mobile/generateOTP|Generate Mobile OTP to start mobile txn.
|||8.2.2|v2/account/profile/deactivate|Deactivate the account using mobile or aadhaar otp.
||||
8.3|Deactivate ABHA using password|8.3|v2/account/profile/deactivate|Deactivate the account using mobile or aadhaar otp.

