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

## Creation of ABHA Address

1. Using Mobile Number
Registration Flow : ABHA address creation with mobile number flow (Self Declared Flow - without KYC)

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


15|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|
16|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|


2. Using ABHA Number
3. Link/De-link ABHA Address

S.No|Function|Functionality|Test Case|Steps To Be Executed 
|--|----|------|-----|-----|


