+++
title = "PHR Application"
date = 2023-04-26T01:00:25+05:30
weight = 8
chapter = true
pre = "<b>10.4 </b>"
+++

# PHR Application

**Functionalities of PHR Applications:** Creation of ABHA address, Subscriptions for notifications, helping users manage consents, upload of user scanned records and more

{{% badge style="blue"  %}}Mandatory{{% /badge %}} 

{{% badge %}}Optional{{% /badge %}} 

**Using Mobile Number** - Registration Flow : ABHA address creation with mobile number flow (Self Declared Flow - without KYC)

S.No|Functionality|Test Scenario|Steps To Be Executed 
|--|------|-----|-----|
1|{{% badge style="blue"  %}}Mandatory{{% /badge %}} | Click on "Register" to create a new ABHA address||
2|{{% badge style="blue"  %}}Mandatory{{% /badge %}} | Select the "Mobile Number option to create ABHA address via mobile number and click on "Continue" button||
3|{{% badge style="blue"  %}}Mandatory{{% /badge %}} | Enter the mobile number and click on "Continue" button ||
4|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Validate mobile OTP received on entered mobile number |Check if an individual receives mobile OTP to validate mobile no
5|{{% badge style="blue"  %}}Mandatory{{% /badge %}} |Resend mobile OTP after 60 seconds post clicking on "Resend OTP"|Check if an individual receive mobile OTP after 60 seconds and an individual is able to validate mobile number
6|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Display ABHA addresses linked with entered validated mobile number. So that an individul can select an ABHA address in which one wishes to login.|Check if all ABHA addresses linked to mobile no are displayed to select any one and login in PHR application
7|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on "Still want to create a new ABHA address" for creation a new ABHA address| |
8|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Fill following profile details such as: • First Name • Middle Name • Last Name • Date of Birth - Day, Month and Year • Gender • Email ID • Address • State • District • Pin Code | **Mandatory fields:** • First Name  • Year (within Date of Birth) • Gender • Address • State • District • Pin Code. And **Optional fields:** • Middle Name • Last Name • Day (within Date of Birth) • Month (within Date of Birth) • Email ID
9|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on checkbox beside "User Information Agreement" to voluntary share profile details with NHA for creating ABHA address and click on "Continue" button|Check if check box is selected beside user information agreement before clicking on "continue" button .
10|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Create ABHA address as per ABHA address policy. ABHA address policy: Minimum length 4 including alphabet, number & dot (.) are allowed. Number cannot be in beginning and dot (.) cannot be in beginning & end. | Check that adherence to ABHA address policy is must to create ABHA address. 
11|{{% badge %}}Optional{{% /badge %}}|Suggestions to create ABHA address as per an individual's name & username of e-mail ID needs to be displayed while creating it.	| Check if suggestions of ABHA address are displayed while creating it. Display "already taken" if entered ABHA address is already created by some other individual. Because no two ABHA address can be same.
12|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Create password, confirm password and click on "Submit" button. Password needs to be created as per password policy. Password policy: 8 characters or longer, one A-Z, one a-z, one 0-9, atleast one symbol, no space and not more than 2 consecutive characters or keyboard keys. | Check that adherence to password policy is must to create ABHA address. 
13|{{% badge style="blue"  %}}Mandatory{{% /badge %}}| Congratulation Screen is displayed stating "Congratulations! ABHA address is created successfully " and click on "Login" button| Check that congratulations message is displayed after creating ABHA address & password. Also, an individual should able to login with updated ABHA address and password.
14|{{% badge style="blue"  %}}Mandatory{{% /badge %}}| Provide Consent after clicking on login button. Click on "I Agree" against "Personal Data Processing Consent Form". Post this user is able to successfully Login	| Check that when an individual login for first time, post agreeing to the "Personal Data Processing Consent Form" an individual is able to login.


**ABHA address creation with email ID flow** - Registration Flow : ABHA address creation with email ID flow (Self Declared Flow - without KYC)

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on "Register" to create a new ABHA address||
2.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Select the "Email ID" option to create ABHA address via email ID and click on "Continue" button||
3.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Enter the e-mail id and click on "Continue" button||
4.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Validate e-mail OTP received on entered e-mail ID|Check if an individual receives e-mail OTP to validate e-mail ID
5.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Resend e-mail OTP after 60 seconds post clicking on "Resend OTP"|Check if an individual receive e-mail OTP after 60 seconds and an individual is able to validate the e-mail ID
6.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Display ABHA addresses linked with entered validated e-mail id. So that an individul can choose an ABHA address in which one wishes to login.	| Check if all ABHA addresses linked to e-mail ID are displayed to select any one and login in PHR app
7.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on "Still want to create a new ABHA address" for creation a new ABHA address ||
8.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Fill following profile details such as: • First Name • Middle Name • Last Name • Date of Birth - Day, Month and Year • Gender • Email ID • Address • State • District • Pin Code |	Check that an individual can create ABHA address only when mandatory fields are filled. 
9.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on checkbox beside "User Information Agreement" to voluntary share profile details with NHA for creating ABHA address and click on "Continue" button| Check if check box is selected beside user information agreement before clicking on "continue" button .  
10.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Create ABHA address as per ABHA address policy. ABHA address policy: Minimum length 4 including alphabet, number & dot (.) are allowed. Number cannot be in beginning and dot (.) cannot be in beginning & end. |	Check that adherence to ABHA address policy is must to create ABHA address. 
11.|{{% badge %}}Optional{{% /badge %}}|Suggestions to create ABHA address as per an individual's name & username of e-mail ID needs to be displayed while creating it.	| Check if suggestions of ABHA address are displayed while creating it. Display "already taken" if entered ABHA address is already created by some other individual. Because no two ABHA address can be same.
12.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|"Create password, confirm password and click on "Submit" button. Password needs to be created as per password policy. (Check remark column) Password policy: 8 characters or longer, one A-Z, one a-z, one 0-9, atleast one symbol, no space and not more than 2 consecutive characters or keyboard keys. | Check that adherence to password policy is must to create ABHA address. 
13.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}| Congratulation Screen is displayed stating "Congratulations! ABHA address is created successfully " and click on "Login" button	| Check that congratulations message is displayed after creating ABHA address & password. Also, an individual should able to login with updated ABHA address and password.
14.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on "I Agree" against "Personal Data Processing Consent Form". Post this user is able to successfully Login	| Check that when an individual login for first time, post agreeing to the "Personal Data Processing Consent Form" an individual is able to login.

**Using ABHA Number** - Registration Flow : ABHA address creation with ABHA number flow (KYC verified flow)
S.No|Functionality|Test Scenario|Steps To Be Executed 
|--|------|-----|-----|
1.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on "Register" to create a new ABHA address||
2.| {{% badge style="blue"  %}}Mandatory{{% /badge %}}|Select the "ABHA number" option to create ABHA address via ABHA number and click on "Continue" button||
3.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Enter the 14 - digit ABHA number and click on "Continue" button||
4.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Validate ABHA number by entering aadhar OTP/mobile OTP received on mobile number linked with entered ABHA number. | Check if an individual receives aadhar OTP/mobile OTP and able to validate the ABHA no. 
5.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Resend aadhar OTP / mobile OTP after 60 seconds.|Check if an individual receive aadhar OTP / mobile OTP after 60 seconds and an individual is able to validate the ABHA no by entering the OTP. 
6.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Display ABHA addresses linked with entered validated ABHA number. So that an individul can select an ABHA address in which one wishes to login.|Check if all ABHA addresses linked to ABHA no are displayed to select any one and login in PHR app
7.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on "Still want to create a new ABHA address" for creation a new ABHA address ||
8.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|"Following profile details are auto-populated from ABHA portal: • First Name • Middle Name • Last Name  • Date of Birth - Day, Month and Year • Gender • Mobile number • Email ID • Address • State • District • Pin Code | Check that all profile details are popultated from ABHA side to PHR app. 
9.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on checkbox beside "User Information Agreement" to voluntary share profile details with NHA for creating ABHA address and click on "Continue" button. | Check if check box is selected beside user information agreement before clicking on "continue" button .  
10.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Create ABHA address. ABHA address needs to be created as per ABHA address policy. ABHA address policy: Minimum length 4 including alphabet, number & dot (.) are allowed. Number cannot be in beginning and dot (.) cannot be in beginning & end. | Check that adherence to ABHA address policy is must to create ABHA address. 
11.|{{% badge %}}Optional{{% /badge %}}|Suggestions to create ABHA address as per an individual's name & username of e-mail ID needs to be displayed while creating it.	| Check if suggestions of ABHA address are displayed while creating it. Display "already taken" if entered ABHA address is already created by some other individual. Because no two ABHA address can be same.
12.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Create password, confirm password and click on "Submit" button. Password needs to be created as per password policy. Password policy:  8 characters or longer, one A-Z, one a-z, one 0-9, atleast one symbol, no space and not more than 2 consecutive characters or keyboard keys. | Check that adherence to password policy is must to create ABHA address. 
13.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Congratulation Screen is displayed stating "Congratulations! ABHA address name@abdm is created successfully " and click on "Login" button| Check that congratulations message is displayed after creating ABHA address & password. Also, an individual should able to login with updated ABHA address and password.
14.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on "I Agree" against "Personal Data Processing Consent Form". Post this user is able to successfully Login |	Check that when an individual login for first time, post agreeing to the "Personal Data Processing Consent Form" an individual is able to login.


**ABHA number creation with KYC** - ABHA number creation with KYC such as aadhar, DL, etc. Suppose an individual is creating ABHA number using Aadhar as KYC

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}| Visit - https://abha.abdm.gov.in/ and click on "Create ABHA number
2.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on option (aadhar / DL) through which an individual wants to create the ABHA no. Suppose an individual select aadhar as an option to create the ABHA no. Ensure that aadhar is linked to mobile no as aadhar OTP authentication is needed to create ABHA no with aadhar flow. 
3.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Enter 12 - digit aadhar no and provide consent to voluntary share aadhar demographic information for creation of ABHA number|Check that aadhar OTP is received on mobile no linked with aadhar
4.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Validate the entered aadhar no by entering the OTP received on mobile no linked to aadhar. | Check that validation of aadhar no is successful after entering the correct aadhar OTP 
5.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Resend aadhar OTP after 60 seconds.| Check if an individual receive aadhar OTP after 60 seconds and an individual is able to validate the ABHA no by entering the OTP. 
6.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|ABHA number card is created using aadhar demographic information. Click on "Download ABHA number card" to download the ABHA number card. All details in the ABHA number card are as per aadhar KYC. | Check that ABHA number card is created and it can also be downloaded. Also, check that all information in card is as per aadhar KYC. 


**Login Flow** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with mobile number flow|Enter mobile number linked with ABHA address||
2.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with mobile number flow|Validate mobile number via mobile OTP	| Check if an individual receives mobile OTP and able to login with mobile number
3.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with mobile number flow|Resend Mobile OTP after 60 seconds post clicking on "Resend OTP". ||
4.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with mobile number flow|Display ABHA addresses linked with entered validated mobile number. So that an individul can select an ABHA address in which one wishes to login.	||
5.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with e-mail ID flow	| Enter e-mail ID linked with ABHA address
6.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with e-mail ID flow	| Validate e-mail ID via e-mail OTP|Check if an individual receive email OTP and login with e-mail OTP
7.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with e-mail ID flow| Resend e-mail OTP after 60 seconds post clicking on "Resend OTP"|Check if an individual receive email OTP after 60 seconds  and login with e-mail OTP
8.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with e-mail ID flow	| Display ABHA addresses linked with entered validated e-mail ID. So that an individul can select an ABHA address in which one wishes to login.|Check if all ABHA addresses linked with entered email ID are displayed and an individual is able to login in selected ABHA address
9.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with easy to remember ABHA address (name@abdm) flow|Enter easy to remember ABHA address - name@abdm||
10.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with easy to remember ABHA address (name@abdm) flow|Validate ABHA address via password / mobile OTP / e-mail OTP / aadhar OTP as per auth mode|Check if an individual is able to login with easy to remember ABHA address via password
11.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with easy to remember ABHA address (name@abdm) flow|Validate ABHA address via password / mobile OTP / e-mail OTP / aadhar OTP as per auth mode|Check if an individual is able to login with easy to remember ABHA address via mobile OTP / e-mail OTP / aadhar OTP as per auth mode
12.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with easy to remember ABHA address (name@abdm) flow|Resend aadhar OTP / mobile OTP / e-mail OTP after clicking on "Resend OTP"|Check if an individual receive aadhar OTP / mobile OTP/e-mail OTP after 60 seconds and an individual is able to login post validation of ABHA address
13.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with default ABHA address (14-digit@abdm) flow|Enter default ABHA address such as 14-digit@abdm||
14.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with default ABHA address (14-digit@abdm) flow|Validate ABHA address via mobile OTP / aadhar OTP | Check if aadhar OTP / mobile OTP is received and post validation of ABHA number, an individual is able to successfully login 
15.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with default ABHA address (14-digit@abdm) flow|Resend aadhar OTP / mobile OTP after clicking on "Resend OTP" | Check if an individual receive aadhar OTP / mobile OTP after 60 seconds and an individual is able to login post validation of ABHA address
16.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with ABHA number flow|Enter 14 digit ABHA number||
17.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with ABHA number flow|Validate ABHA number via aadhar OTP / mobile OTP	| Check if aadhar OTP / mobile OTP is received and post validation of ABHA number, an individual is able to successfully login 
18.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with ABHA number flow| Resend aadhar OTP / mobile OTP after clicking on "Resend OTP"| Check if an individual receive aadhar OTP / mobile OTP after 60 seconds and an individual is able to login post validation of ABHA number
19.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Reset Password|Login with any mode - mobile number / email ID / default ABHA address / easy to remember ABHA address / ABHA number|Check if password can be updated by an individual post login with any mode
20.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Reset Password|Post successful login, click on reset password withing setting of the menu bar||
21.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Reset Password|Create password as per password policy. Password policy: 8 characters or longer, one A-Z, one a-z, one 0-9, atleast one symbol, no space and not more than 2 consecutive characters or keyboard keys. | Check if password is created as per password policy
22.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Reset Password|Confirm password	| Check new password is created only after same password is confirmed again
23.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Reset Password|A message is displayed called "Your password is successfully changed" | Check if an individual new password is created by login with new password


**Health and Facility records linking: User initiated linking flow (Discovery Flow) - Complete Discovery of HIP, linking, fetching and viewing of records in PHR app** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Link HIP|After Login : Click on "Link my Health Records" tab in "My Records" tab|Click on "Link my Health Records" tab / "+" symbol in "Linked Facility" tab to search records in HIP
2.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Discover HIP|Search HIP 's such as hospital, clinic, lab to discover them based on typed string by the individual|When individual will search the visited facilty (HIP), the entire facilty name with complete address will be discovered by the individual. This "Search" is based on string, i.e HIP name entered by the patient in the search bar of PHR app.
3.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Display of patient details	| After searching facility: The details visible to patient on the PHR app are: Verified mobile number, ABHA address, ABHA number, Patient ID, Full Name, Year of Birth, Gender. | Details of Patient will be visible when individual search for the HIP in PHR app while user initiated linking flow.
4.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Fill Patient ID (Optional)	| This customizable lable is: Patient ID - In case of linking health records created at health facility. And this field is optional for patient to enter. | Check, if exact match of record is found after entering correct Patient ID 
5. | {{% badge style="blue"  %}}Mandatory{{% /badge %}}  Matching of API specifications to link record | Click on "Fetch Records". After matching following fields, records will be fetched from facility (HIP) to PHR app: Name (Mandatory), Year of Birth (Mandatory), Gender (Mandatory), Mobile Number (Mandatory), Patient ID (Optional) | Ensure that already linked care context should not be discovered in PHR mobile app. If all care context of discovered facilty are already linked, then display message called ""All your existing records are linked. No additional records availaible for linking". Ensure that the linked care context is shown in the ""Linked Facility"" tab of the PHR mobile app
6.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Link records|Display of records details like HI type | Display of all correct details of records, after matching of API specifications. Select the record which patient wants to link and click on "Link Selected"
7.|{{% badge %}}Optional{{% /badge %}}  Fill mobile OTP received to complete linking of record. | Mobile OTP will be received once individual clicks on fetch records. After successful validation of OTP, display message called “Records are successfully linked”. This OTP is sent by HIP to the patient's mobile. | Fill mobile OTP for successful linking of facility. Error message display, for following scenarios : **Scenario 1:** If there is Communication Gap, between HIP and individual – Due to some technical issue at HIP end like if server is down then, error message is displayed as “Couldn’t Connect: We are sorry. Unable to contact your hospital. Please try again later”. **Scenario 2:** If individual have never visited the hospital – An error message is displayed as “No health records found”. **Scenario 3:** Records of all visits are already linked and there is nothing new to link - – An error message is displayed as “No new health record to link: Records of all visits are already linked and there is nothing new to link
8.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Linked facility will be visible in "Linked Facility" tab. Click on "Pull Records" button to fetch and view records.| Ensure that the patient's health-records are getting fetched. | 1. Check that PHR app sends data transfer request to HIP within 5 minutes after an individual click on "Pull Records" button. 2. Ensure that the patient health records are fetched within 2 hours in the PHR mobile app. Ensure that the patient's health-records are fetched without ERRORED"
9.|{{% badge %}}Optional{{% /badge %}}  Display message regarding fetching of records may take time in "My Records" tab | 1. Keep "I" button in ""My Records"", so that message is displayed regarding fetching of records may take time when patient hovers over i button. 2. Check that proper error or status message will be displayed if records are taking time in fetching. For e.g. Refresh to fetch record, Data fetch in progress etc.."|Since, fetching of records take time. Display message called "Recently linked records might take some time to show" when patient hover over "i button" in "My Records" tab.
10. | {{% badge %}}Optional{{% /badge %}} Records will be displayed in "My Records" tab. | Click on the attached report to view the health record. | After clicking on record: Details of health record will be displayed alongwith an attachment consisting of record. Details of health record included structured data such as: Facility Name, Visit type, Prescribed By, Date and Time
11.| {{% badge %}}Optional{{% /badge %}} View record in mobile device |	Record will open when individual clicks on the attachment consisting health record | Records will open in the device and patient can view it


**ABHA number creation with KYC** - ABHA number creation with KYC such as aadhar, DL, etc. Suppose an individual is creating ABHA number using Aadhar as KYC

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|


