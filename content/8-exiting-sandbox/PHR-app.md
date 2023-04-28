+++
title = "PHR Application"
date = 2023-04-26T01:00:25+05:30
weight = 8
chapter = true
pre = "<b>8.4 </b>"
+++

# PHR Application

**Functionalities of PHR Applications:** Creation of ABHA address, Subscriptions for notifications, helping users manage consents, upload of user scanned records and more


**Using Mobile Number** - Registration Flow : ABHA address creation with mobile number flow (Self Declared Flow - without KYC)

S.No|Functionality|Test Scenario|Steps To Be Executed 
|--|------|-----|-----|
1|{{% badge style="blue"  %}}Mandatory{{% /badge %}} | Click on "Register" to create a new ABHA address||
2|{{% badge style="blue"  %}}Mandatory{{% /badge %}} | Select the "Mobile Number option to create ABHA address via mobile number and click on "Continue" button||
3|{{% badge style="blue"  %}}Mandatory{{% /badge %}} | Enter the mobile number and click on "Continue" button ||
4|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Validate mobile OTP received on entered mobile number |Check if an individual receives mobile OTP to validate mobile no
5|{{% badge style="blue"  %}}Mandatory{{% /badge %}} |Resend mobile OTP after 60 seconds post clicking on "Resend OTP|Check if an individual receive mobile OTP after 60 seconds and an individual is able to validate mobile number
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
5.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Resend e-mail OTP after 60 seconds post clicking on "Resend OTP|Check if an individual receive e-mail OTP after 60 seconds and an individual is able to validate the e-mail ID
6.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Display ABHA addresses linked with entered validated e-mail id. So that an individul can choose an ABHA address in which one wishes to login.	| Check if all ABHA addresses linked to e-mail ID are displayed to select any one and login in PHR app
7.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on "Still want to create a new ABHA address" for creation a new ABHA address ||
8.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Fill following profile details such as: • First Name • Middle Name • Last Name • Date of Birth - Day, Month and Year • Gender • Email ID • Address • State • District • Pin Code |	Check that an individual can create ABHA address only when mandatory fields are filled. 
9.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on checkbox beside "User Information Agreement" to voluntary share profile details with NHA for creating ABHA address and click on "Continue" button| Check if check box is selected beside user information agreement before clicking on "continue" button .  
10.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Create ABHA address as per ABHA address policy. ABHA address policy: Minimum length 4 including alphabet, number & dot (.) are allowed. Number cannot be in beginning and dot (.) cannot be in beginning & end. |	Check that adherence to ABHA address policy is must to create ABHA address. 
11.|{{% badge %}}Optional{{% /badge %}}|Suggestions to create ABHA address as per an individual's name & username of e-mail ID needs to be displayed while creating it.	| Check if suggestions of ABHA address are displayed while creating it. Display "already taken" if entered ABHA address is already created by some other individual. Because no two ABHA address can be same.
12.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Create password, confirm password and click on "Submit" button. Password needs to be created as per password policy. (Check remark column) Password policy: 8 characters or longer, one A-Z, one a-z, one 0-9, atleast one symbol, no space and not more than 2 consecutive characters or keyboard keys. | Check that adherence to password policy is must to create ABHA address. 
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
8.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Following profile details are auto-populated from ABHA portal: • First Name • Middle Name • Last Name  • Date of Birth - Day, Month and Year • Gender • Mobile number • Email ID • Address • State • District • Pin Code | Check that all profile details are popultated from ABHA side to PHR app. 
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
7.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with e-mail ID flow| Resend e-mail OTP after 60 seconds post clicking on "Resend OTP|Check if an individual receive email OTP after 60 seconds  and login with e-mail OTP
8.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with e-mail ID flow	| Display ABHA addresses linked with entered validated e-mail ID. So that an individul can select an ABHA address in which one wishes to login.|Check if all ABHA addresses linked with entered email ID are displayed and an individual is able to login in selected ABHA address
9.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with easy to remember ABHA address (name@abdm) flow|Enter easy to remember ABHA address - name@abdm||
10.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with easy to remember ABHA address (name@abdm) flow|Validate ABHA address via password / mobile OTP / e-mail OTP / aadhar OTP as per auth mode|Check if an individual is able to login with easy to remember ABHA address via password
11.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with easy to remember ABHA address (name@abdm) flow|Validate ABHA address via password / mobile OTP / e-mail OTP / aadhar OTP as per auth mode|Check if an individual is able to login with easy to remember ABHA address via mobile OTP / e-mail OTP / aadhar OTP as per auth mode
12.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with easy to remember ABHA address (name@abdm) flow|Resend aadhar OTP / mobile OTP / e-mail OTP after clicking on "Resend OTP|Check if an individual receive aadhar OTP / mobile OTP/e-mail OTP after 60 seconds and an individual is able to login post validation of ABHA address
13.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with default ABHA address (14-digit@abdm) flow|Enter default ABHA address such as 14-digit@abdm||
14.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with default ABHA address (14-digit@abdm) flow|Validate ABHA address via mobile OTP / aadhar OTP | Check if aadhar OTP / mobile OTP is received and post validation of ABHA number, an individual is able to successfully login 
15.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with default ABHA address (14-digit@abdm) flow|Resend aadhar OTP / mobile OTP after clicking on "Resend OTP" | Check if an individual receive aadhar OTP / mobile OTP after 60 seconds and an individual is able to login post validation of ABHA address
16.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with ABHA number flow|Enter 14 digit ABHA number||
17.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with ABHA number flow|Validate ABHA number via aadhar OTP / mobile OTP	| Check if aadhar OTP / mobile OTP is received and post validation of ABHA number, an individual is able to successfully login 
18.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with ABHA number flow| Resend aadhar OTP / mobile OTP after clicking on "Resend OTP| Check if an individual receive aadhar OTP / mobile OTP after 60 seconds and an individual is able to login post validation of ABHA number
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
5. | {{% badge style="blue"  %}}Mandatory{{% /badge %}}  Matching of API specifications to link record | Click on "Fetch Records". After matching following fields, records will be fetched from facility (HIP) to PHR app: Name (Mandatory), Year of Birth (Mandatory), Gender (Mandatory), Mobile Number (Mandatory), Patient ID (Optional) | Ensure that already linked care context should not be discovered in PHR mobile app. If all care context of discovered facilty are already linked, then display message called "All your existing records are linked. No additional records availaible for linking". Ensure that the linked care context is shown in the "Linked Facility" tab of the PHR mobile app
6.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Link records|Display of records details like HI type | Display of all correct details of records, after matching of API specifications. Select the record which patient wants to link and click on "Link Selected"
7.|{{% badge %}}Optional{{% /badge %}}  Fill mobile OTP received to complete linking of record. | Mobile OTP will be received once individual clicks on fetch records. After successful validation of OTP, display message called “Records are successfully linked”. This OTP is sent by HIP to the patient's mobile. | Fill mobile OTP for successful linking of facility. Error message display, for following scenarios : **Scenario 1:** If there is Communication Gap, between HIP and individual – Due to some technical issue at HIP end like if server is down then, error message is displayed as “Couldn’t Connect: We are sorry. Unable to contact your hospital. Please try again later”. **Scenario 2:** If individual have never visited the hospital – An error message is displayed as “No health records found”. **Scenario 3:** Records of all visits are already linked and there is nothing new to link - – An error message is displayed as “No new health record to link: Records of all visits are already linked and there is nothing new to link
8.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Linked facility will be visible in "Linked Facility" tab. Click on "Pull Records" button to fetch and view records.| Ensure that the patient's health-records are getting fetched. | 1. Check that PHR app sends data transfer request to HIP within 5 minutes after an individual click on "Pull Records" button. 2. Ensure that the patient health records are fetched within 2 hours in the PHR mobile app. Ensure that the patient's health-records are fetched without ERRORED"
9.|{{% badge %}}Optional{{% /badge %}}  Display message regarding fetching of records may take time in "My Records" tab | 1. Keep "I" button in "My Records", so that message is displayed regarding fetching of records may take time when patient hovers over i button. 2. Check that proper error or status message will be displayed if records are taking time in fetching. For e.g. Refresh to fetch record, Data fetch in progress etc..|Since, fetching of records take time. Display message called "Recently linked records might take some time to show" when patient hover over "i button" in "My Records" tab.
10. | {{% badge %}}Optional{{% /badge %}} Records will be displayed in "My Records" tab. | Click on the attached report to view the health record. | After clicking on record: Details of health record will be displayed alongwith an attachment consisting of record. Details of health record included structured data such as: Facility Name, Visit type, Prescribed By, Date and Time
11.| {{% badge %}}Optional{{% /badge %}} View record in mobile device |	Record will open when individual clicks on the attachment consisting health record | Records will open in the device and patient can view it


**Health Programme records linking, fetching and viewing of records: User initiated linking (Discovery Flow)** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Link Programme	| After Login : Click on "Link my Health Records" tab in "My Records" section|Click on "Link my Health Records" tab / "+" symbol in "Linked Facility" tab to search records in HIP.
2.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Select Health Programme|Select programme name whose record patient wants to link, fetch and view in PHR app. Currently, government health programmes such as "CoWIN", "AB-PMJAY", e-Sanjeevani OPD, e-Sanjeevani HWC, RCH programme. Going forward, other health programmes will also integrate with PHR app"	| Check, if patient is able to select the integrated government health programme with the PHR app.
3. | {{% badge style="blue"  %}}Mandatory{{% /badge %}}  Display of patient details	| After clicking on programme name, the details visible to patient are: Verified mobile number, ABHA address, ABHA number, CoWIN registered mobile no (Customizable Label - Optional), Full Name, Year of Birth, Gender	| In User initiated linking (Discovery Flow), details of patient will be visible when individual select government health programme in PHR app.
4. | {{% badge style="blue"  %}}Mandatory{{% /badge %}}  Fill PM-JAY ID (Optional) | This customizable label is: 1. PMJAY ID - In case of linking health records from AB-PMJAY programme. 2. CoWIN Registered Mobile No - In case of linking health records from CoWIN. | Check, if exact match of patient records are found, after entering correct PMJAY ID / CoWIN registered mobile number
5. | {{% badge style="blue"  %}}Mandatory{{% /badge %}}  Matching of API specifications | "Click on "Fetch Records". After matching following fields, records will be fetched from programme to PHR mobile app: Name (Mandatory), Year of Birth (Mandatory), Gender (Mandatory), Mobile Number (Mandatory), Patient ID (Optional)	| Ensure that already linked care context should not be discovered in PHR mobile app. If all care context of selected government health programme are already linked, then display message called "All your existing records are linked. No additional records availaible for linking". Ensure that the linked care context is shown in the "Linked Facility" tab of the PHR mobile app
6.| {{% badge style="blue"  %}}Mandatory{{% /badge %}}  Link records	| Display of records details such as Dose 1, Dose 2 and Dose 3 (Precautionary dose) in case of CoWIN programme. | Display of all correct details of records, after matching of API specifications
7.| {{% badge style="blue"  %}}Mandatory{{% /badge %}} 	Display of records details such as Dose 1, Dose 2 and Dose 3 (Precautionary dose) in case of CoWIN programme. | Select the record which patient wants to link and click on "Link Selected"
8. | {{% badge %}}Optional{{% /badge %}} Fill mobile OTP received to complete linking of record. | Mobile OTP will be received once individual clicks on fetch records. After successful validation of OTP, display message called “Records are successfully linked”. This OTP is sent by government health programme to the patient's mobile. | Fill mobile OTP for successful linking of facility.
9.|{{% badge %}}Optional{{% /badge %}} Fill mobile OTP received to complete linking of record. | Mobile OTP will be received once individual clicks on fetch records. After successful validation of OTP, display message called “Records are successfully linked”. This OTP is sent by government health programme to the patient's mobile. | Fill mobile OTP for successful linking of facility 
10.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Linked programme will be visible in "Linked Facility" tab. Click on "Pull Records" button to fetch and view records|Ensure that the patient's health-records are getting fetched|1. Check that PHR app sends data transfer request to HIP within 5 minutes after an individual click on "Pull Records" button. 2. Ensure that the patient health records are fetched within 2 hours in the PHR mobile app
11.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Linked programme will be visible in "Linked Facility" tab. Click on "Pull Records" button to fetch and view records|Ensure that the patient's health-records are getting fetched|Ensure that the patient's health-records are fetched without ERRORED
12.|{{% badge %}}Optional{{% /badge %}}  Display message regarding fetching of records may take time in "My Records" tab. |1. Keep "I" button in "My Records", so that message is displayed regarding fetching of records may take time when patient hovers over i button. 2. Check that proper error or status message will be displayed if records are taking time in fetching. For e.g. Refresh to fetch record, Data fetch in progress etc. | Since, fetching of records take time. Display message called "Recently linked records might take some time to show" when patient hover over "i button" in "My Records" tab.
13. | {{% badge %}}Optional{{% /badge %}} Records will be displayed in "My Records" tab. Click on the attached report to view the health record.|After clicking on record: Details of health record will be displayed alongwith an attachment consisting of record	| Details of health record included structured data such as: Facility Name, Visit type, Prescribed By, Date and Time
14. | {{% badge %}}Optional{{% /badge %}} View record in mobile device |	Record will open when individual clicks on the attachment consisting health record|Records will open in the device and patient can view it



**HIP initiated linking flow**  - When health records are linked with ABHA address at the health facility / health programme

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1|{{% badge style="blue" %}}Mandatory{{% /badge %}}  Post linking of health records with ABHA address by the HIP with patient consent| the individual can view the health records on the PHR mobile app|Health data will be visible in PHR app once HIP link health records with the ABHA address.|Once Individual visits the hospital. • ABHA address is shared with the health programme / health facility. • Individual validates the ABHA address with the mobile OTP. • Post linking of health records with ABHA address by the HIP| the individual can open any PHR app  and click on "Pull Records" button against the visited health programme / health facility| where the record is created and linked to ABHA address to view the record in mobile device.

**Sharing of health records with patient's consent to the HIU** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = DiagnostocReport Structured)||||||||||||
2|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = DiagnostocReport Un-Structured)||||||||||||
3|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = Prescription-Structured)||||||||||||
4|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = Prescription-Un-Structured)||||||||||||
5|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = DischargeSummary-Structured)||||||||||||
6|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = DischargeSummary-Un-Structured)||||||||||||
7|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = CosultingNote-Structured)||||||||||||
8|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient. (HI Type = CosultingNote-Un-Structured)||||||||||||
9|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient. (HI Type = Immunization record-Structured)||||||||||||
10|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient. (HI Type = Immunization record-Un-Structured)||||||||||||
11|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient/ (HI Type = Wellness Record-Structured)||||||||||||
12|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient. (HI Type = Wellness Record-Un-Structured)||||||||||||
13|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient. (HI Type = Health Record-Structured)||||||||||||
14|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient. (HI Type = Health Record-Un-Structured)

**Display Profile Details with status as KYC Verified / Self-Declared**

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}} Showing individual's profile details in the PHR app|Individual's profile is displayed in the PHR app with their status such as KYC verified and Self-Declared. | Display all profile details filled to the individual, when individual click on Profile after Login. Also| display KYC Verified" with green tick mark for those profiles where ABHA address is linked with ABHA number. Display Self Delared with exclaimation mark for those profiles where ABHA address is not linked with ABHA number. ABHA number is visible in KYC verified profile and ABHA number is not visible in Self-Declared profile.


**Download ABHA address card in the PDF format** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}} Download ABHA address card | Post clicking on "QR Code" icon, an individual can scan QR Code, share ABHA address card and download ABHA address card | Following fields will be displayed in the ABHA address card: Profile Photo, Full Name, ABHA number - It will be displayed if, 14-digit Health ID number is linked to the ABHA address. ABHA number is displayed as XX-XXXX-XXXX-3421 (Hide starting 12 digits of ABHA number), ABHA address  - It will be displayed as XXXXam@abdm (Hide starting alphabets of ABHA address), QR Code, Date of Birth, Gender, Mobile Number - It will be displayed as XXXXXX2278 (Hide starting 6 digits of ABHA number)


**Consent Pin** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1|{{% badge style="blue" %}}Mandatory{{% /badge %}} Set Consent Pin|Validate OTP received on registered mobile number|Check that OTP is received on registered mobile number. 
2|{{% badge style="blue" %}}Mandatory{{% /badge %}} Set Consent Pin|Validate OTP received on registered mobile number|Resend OTP option is provided| if OTP is not received on mobile in 60 seconds
3|{{% badge style="blue" %}}Mandatory{{% /badge %}} Set Consent Pin|Enter 4 digit consent pin|Check that only 4 digit consent pin is accepted 
4|{{% badge style="blue" %}}Mandatory{{% /badge %}} Set Consent Pin|Confirm Consent Pin|Re-enter the consent pin to confirm the consent pin. Check that confirmation of consent pin is taken by re-entering it.
5|{{% badge style="blue" %}}Mandatory{{% /badge %}} Set Consent Pin|Display message, so that an individual knows that consent pin is set successfully|Display message "Congratulations! Your consent pin is successfully updated". Below this message "Go Back To Home Screen" tab is provided to navigate the individual to home screen.
6|{{% badge style="blue" %}}Mandatory{{% /badge %}} Reset Consent Pin|Enter 4 digit old consent pin|Check if old consent pin entered is correct
7|{{% badge style="blue" %}}Mandatory{{% /badge %}} Reset Consent Pin|Enter 4 digit new consent pin|Check that only 4 digit consent pin are accepted
8|{{% badge style="blue" %}}Mandatory{{% /badge %}} Reset Consent Pin|Confirm new consent pin|Re-enter the consent pin to confirm the consent pin. Check that confirmation of consent pin is taken by re-entering it.
9|{{% badge style="blue" %}}Mandatory{{% /badge %}} Reset Consent Pin|Display message, so that an individual knows that consent pin is updated|Display message Congratulations! Your new consent pin is successfully updated. Below this message "Go Back To Home Screen tab is provided to navigate the individual to home screen.
10|{{% badge style="blue" %}}Mandatory{{% /badge %}} Forgot Consent Pin|Enter OTP|Check that OTP is received on registered mobile number. 
11|{{% badge style="blue" %}}Mandatory{{% /badge %}} Forgot Consent Pin|Resend OTP, if OTP is not received in 60 seconds|Check that resend OTP option is provided, if OTP is not received on mobile device
12|{{% badge style="blue" %}}Mandatory{{% /badge %}} Forgot Consent Pin|Enter 4 digit new consent pin|4 digit consent pin is only accepted 
13|{{% badge style="blue" %}}Mandatory{{% /badge %}} Forgot Consent Pin|Confirm new consent pin|Re-enter the consent pin to confirm the consent pin. Check that confirmation of consent pin is taken by re-entering it.
14|{{% badge style="blue" %}}Mandatory{{% /badge %}} Forgot Consent Pin|Display message, so that an individual knows that consent pin is updated|Display message "Congratulations! Your new consent pin is successfully updated". Below this message "Go Back To Home Screen" tab is provided to navigate the individual to home screen.


**Tabs in PHR app (My Records/Linked Facility/Consents)** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Requests" section in the "Consents" tab of PHR app|1) Requested - Not yet any action is taken by individual on consent request received from HIU to PHR app. |All request (consent / subscription / locker) sent by HIU to patiet are seen  in "Requested" dropdown within "Requests" section of PHR app
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Requests" section in the "Consents" tab of PHR app|2) Denied - Individual have "Denied" consent request received from HIU to PHR app. |All denied request (consent / subscription / locker) by patient are seen in "Denied" dropdown within "Requests" section of PHR app. 
3| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Requests" section in the "Consents" tab of PHR app|3) Expired -  Requests is expired because patient have not acted on consent request received in PHR app within the time duration set by HIU|All expired request (consent / subscription / locker) by patient are seen in "Expired" dropdown within "Requests" section of PHR app.
4| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Approved" section in the "Consents" tab of PHR app|1) Granted - Patient had granted the consent request received from HIU to PHR app|All granted request (consent / subscription / locker) by patient are seen in "Granted" dropdown within "Approved" section of PHR app. 
5| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Approved" section in the "Consents" tab of PHR app|2) Revoked - Patient had revoked consent requests after granting it in PHR app. |All revoked request (consent / subscription / locker) by patient are seen in "Revoked" dropdown within "Approved" section of PHR app. 
6| {{% badge style="blue" %}}Mandatory{{% /badge %}}  View patient helth records in "My Records" tab of PHR app|To view records, post linking and fetching from healthcare providers (health locker, health facility and health programme)|Click on record fetched in the "My Records" tab
7| {{% badge style="blue" %}}Mandatory{{% /badge %}}  View patient helth records in "My Records" tab of PHR app|To view records, post linking and fetching from healthcare providers (health locker, health facility and health programme) |Details of records are viewed with attachment
8| {{% badge style="blue" %}}Mandatory{{% /badge %}}  View patient helth records in "My Records" tab of PHR app|To view records, post linking and fetching from healthcare providers (health locker, health facility and health programme) |Click on the attachment to view the health record / report in the device
9| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Linked Facility" tab in PHR app| Linked providers includes health lockers| health facility and health programme|Ckeck list of all linked providers are displayed and "Pull Record" button is against each one of them. So that patient can click on it to fetch and view record in "My Records" tab.


**Edit Subscription Request/Disable auto approval request** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit active subscription request|Already granted subscription request can be edited|Check if HI types, types of visit and time period can be edited and saved by clicking on "Save Changes" button"
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Disable auto approval requests|Already granted auto approval policy can be disabled|Check if already granted auto approval policy for health locker can be disabled by clickicking on "Disable" button. Post disble of auto - approval policy|locker request is received from health locker for each record.


**Link/Unlink ABHA no to the ABHA address** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Link ABHA no to the ABHA address|Click on "Link ABHA Number" option provided beside "Self Declared" in home screen 
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Link ABHA no to the ABHA address|Enter 14-digit ABHA no 
3| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Link ABHA no to the ABHA address|Validate ABHA no via aadhar OTP / mobile OTP|Check that an individual is able to validate ABHA no via both aadhar OTP / mobile OTP
4| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Link ABHA no to the ABHA address|Resend OTP| if OTP is not received in 60 seconds|Check that resend OTP option is provided after 60 seconds for both aadhar OTP / mobile OTP
5| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Link ABHA no to the ABHA address|Displaye message: "Congratulations! Your ABHA number is now linked to your existing ABHA address. ABHA number is visible on your profile.|Check that post OTP validation of ABHA no| message is displayed that ABHA no is successfully linked with the ABHA address and ABHA number is visible in profile. Also| ABHA number policy will supersede ABHA address. Hence| profile details will change as per ABHA number. In addition to this| "Self-Declared" status is changed to "KYC Verified" in home screen.
6| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Link ABHA no to the ABHA address|Click on "Go back to home screen" tab to go back to profile|Check that after clicking on "Go back to home screen" tab| an individual is able to go back to home screen
7| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Unlink ABHA no to the ABHA address|Click on "Unlink ABHA Number" option provided beside 14-digit ABHA number in home screen. 
8| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Unlink ABHA no to the ABHA address|Display confirmation message: "Even after unlinking ABHA number| you will still be able to share your health records with healthcare providers through ABHA address. Do you still want to unlink ABHA number XX-XXXX-XXXX-XXXX with your existing ABHA address?" (Yes/No)          |Ckeck that confirmation message is displayed before unlinking ABHA no with ABHA address
9| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Unlink ABHA no to the ABHA address|Validate ABHA no by selecting any one of the option - "OTP is sent on mobile number linked with your aadhar" / "OTP on mobile number linked with your ABHA number|Check that an individual is able to validate ABHA no via OTP received on mobile no linked with aadhar / ABHA no
10| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Unlink ABHA no to the ABHA address|Resend OTP| if OTP is not received in 60 seconds|Check that resend OTP option is provided after 60 seconds for both mobile no linked with aadhar / ABHA no
11| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Unlink ABHA no to the ABHA address|Display message: "ABHA number is unlinked to existing ABHA address. Now| ABHA number is not visible in your profile|Check that post OTP validation of ABHA no| message is displayed that ABHA no is successfully unlinked with the ABHA address and ABHA number is not visible in profile.
12| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Unlink ABHA no to the ABHA address|Click on "Go back to home screen" tab to go back to profile|Check that after clicking on "Go back to home screen" tab| an individual is able to go back to home screen


**Edit Profile** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1.1| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for KYC verified profiles |Update mobile number| Mobile OTP is received on updated mobile no. Post mobile OTP validation, mobile no is updated. 
1.2| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for KYC verified profiles |Update email ID| E-mail OTP is received on updated e-mail ID. Post e-mail OTP validation, e-mail ID is updated. 
1.3| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for KYC verified profiles |Update address| All fields of address such as address line 1, district, state and pin-code can be updated. 
1.4| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update Photo|Photo can be edited by an individul taking the picture from mobile camera / upload photo from gallery of the device 
1.5| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update Full Name| Update First Name, Middle name and Last Name
1.6| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update Gender | Update Gender
1.7| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update DoB| Update Day, Month and Year
1.8| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update Mobile No| Mobile OTP is received on updated mobile no. Post mobile OTP validation, mobile no is updated.
1.9| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update Email ID| E-mail OTP is received on updated e-mail ID. Post e-mail OTP validation, e-mail ID is updated.  
1.1| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update Address| All fields of address such as address line 1, district, state and pin-code can be updated. 



**Deep Link Flow** : Send SMS to patient mobile to initiate record linking and fetching in PHR app

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1.1| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | In case patient visits the health facility and do not provide the ABHA address for linking of health records. Then, ABDM compliant health facility will notify ABDM when there is a new health record created of the patient. ABDM will send a deep link SMS is to the patient's mobile for fetching and viewing records in PHR app using User Initiated Linking Flow (Discovery Flow) | Patient visits a health facility and registers by providing Name, DoB, Gender and Mobile. Patient does not share any ABHA Address with the facility.
1.2| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | In case patient visits the health facility and do not provide the ABHA address for linking of health records. Then, ABDM compliant health facility will notify ABDM when there is a new health record created of the patient. ABDM will send a deep link SMS is to the patient's mobile for fetching and viewing records in PHR app using User Initiated Linking Flow (Discovery Flow) | If the Health Facility is participating in ABDM, then it will notify ABDM when there is a new health record for this patient. Only the mobile number and the ID of the facility is notified. Facilities are identified by the facility’s HIPCODE. This can be obtained by registering the facility using the Health Facility Registry and linking the facility to a ABDM approved Health Repository Provider Software.
1.3| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | In case patient visits the health facility and do not provide the ABHA address for linking of health records. Then, ABDM compliant health facility will notify ABDM when there is a new health record created of the patient. ABDM will send a deep link SMS is to the patient's mobile for fetching and viewing records in PHR app using User Initiated Linking Flow (Discovery Flow) | ABDM will send an SMS to the user with a deep link as shown below: Dear Madam/Sir, (facility name) is now participating in Ayushman Bharat Digital Mission (ABDM). Your report at this facility is now ready. See your record by clicking on on phr.abdm.gov.in/uhi/(hipcode) ABDM|NHA
1.4| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | In case patient visits the health facility and do not provide the ABHA address for linking of health records. Then, ABDM compliant health facility will notify ABDM when there is a new health record created of the patient. ABDM will send a deep link SMS is to the patient's mobile for fetching and viewing records in PHR app using User Initiated Linking Flow (Discovery Flow) |Clicking on the link will show the list of all ABDM compliant PHR applications.

**Post clicking on deep link by patient** 

Use Case 1: In case ABDM compliant PHR application is not installed in PHR app, then user is redirected to download and install it from play store/app store."

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | Post clicking on deep link by patient| Check that, if no ABDM compliant PHR application is installed in phone - Navigate patient to play store / app store to install the selected PHR application from the list of all ABDM compliant PHR applications. 
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | Post clicking on deep link by patient| Check that, post installing the PHR app. New user is able to create the ABHA address and Password by providing basic details such as Nma, DoB, Gender, Mobile No., Address 


Use Case 2: In case ABDM compliant PHR application is already installed in PHR app, then app will directly launch and initiate the User Initiated Linking (Discovery Flow)

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | Post clicking on deep link by patient| Check that selected PHR app from the list of all ABDM compliant PHR app's is launched successfully. 
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | Post clicking on deep link by patient| Check that post launch, PHR app initiates the discovery request with HIP where patient health records were created