+++
title = "Using ABHA Number"
date = 2023-03-16T09:30:25+05:30
weight = 4
chapter = true
pre = "<b>5.1.2 </b>"
+++

# Using ABHA Number
|  Applicable To                             |   HMIS / LMIS (PVT)  |   Government Health App  |  
|-------------------------------|:----------------------:|:--------------------:|
|   Using ABHA Number                     |  {{% badge %}}Optional{{% /badge %}}       |  {{% badge %}}Optional{{% /badge %}}         |  

## Functionality Overview

**Description:** Individual enters ABHA address (xyz@abdm), and it is validated depending on auth mode of validation such as mobile OTP/aadhar OTP/email OTP or password to login.

 - In this flow, individual is given an option of creating ABHA address through ABHA (Number) via KYC document. Please note, the list of KYC documents may be revised from time to time.
 - Create an ABHA address of the format abc@abdm via 14-digit ABHA (Number). In this case, profile details like photo, name, date of birth, gender, mobile number, email ID, and address are fetched from the ABHA system.
 - Individual creates an easy to remember ABHA Address along with its password to login
   - Individuals may link/unlink ABHA (Number) with ABHA address as per their choice.


**ABHA Address Policy**

1. ABHA Address Policy:
	- Minimum length is 4 including the allowed alphabet, number & dot(.) 
	- Cannot begin with Number 
	- Cannot begin or end with dot(.) 
	- As a policy, we allow creation of all numeric ABHA addresses for ABHA Number only: 14digit@abdm.

2. 10-digit Mobile number as ABHA Address:
	- For now, we have restricted the creation of (10 digit) MobileNumber@abdm

3. Creation of (14 digit@abdm):
	- ABHA Address is not allowed however, we have the provision for the user to login with the same 14digit@abdm both in web PHR and mobile PHR.

4. Password validation :
	- This has been made optional. You may kindly check the below APIs at your end and reach out to us in case of any issues:
		- Registration via ABHA: /api/v1/phr/registration/hid/create-phr-address
		- Registration via Mobile and Email: /api/v1/phr/registration/create/phr

## Test Cases

**Using ABHA Number** - Registration Flow : ABHA address creation with ABHA number flow (KYC verified flow)
S.No|Functionality|Test Scenario|Steps To Be Executed 
|--|------|-----|-----|
1.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on "Register" to create a new ABHA address||
2.| {{% badge style="blue"  %}}Mandatory{{% /badge %}}|Select the "ABHA number" option to create ABHA address via ABHA number and click on "Continue" button||
3.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Enter the 14 - digit ABHA number and click on "Continue" button||
4.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Validate ABHA number by entering aadhar OTP/mobile OTP received on mobile number linked with entered ABHA number. | Check if an individual receives aadhar OTP/mobile OTP and able to validate the ABHA number. 
5.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Resend aadhar OTP / mobile OTP after 60 seconds.|Check if an individual receive aadhar OTP / mobile OTP after 60 seconds and an individual is able to validate the ABHA number by entering the OTP. 
6.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Display ABHA addresses linked with entered validated ABHA number. So that an individul can select an ABHA address in which one wishes to login.|Check if all ABHA addresses linked to ABHA number are displayed to select any one and login in PHR app
7.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on "Still want to create a new ABHA address" for creation of a new ABHA address ||
8.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Following profile details are auto-populated from ABHA portal: • First Name • Middle Name • Last Name  • Date of Birth - Day, Month and Year • Gender • Mobile number • Email ID • Address • State • District • Pin Code | Check that all profile details are populated from ABHA side to PHR app. 
9.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on checkbox beside "User Information Agreement" to voluntarily share profile details with NHA for creating ABHA address and click on "Continue" button. | Check if check box is selected beside user information agreement before clicking on "continue" button .  
10.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Create ABHA address. ABHA address needs to be created as per ABHA address policy. ABHA address policy: Minimum length 4 including alphabet, number & dot (.) are allowed. Number cannot be in beginning and dot (.) cannot be in beginning & end. | Check that adherence to ABHA address policy is must to create ABHA address. 
11.|{{% badge %}}Optional{{% /badge %}}|Suggestions to create ABHA address as per an individual's name & username of e-mail ID needs to be displayed while creating it.	| Check if suggestions of ABHA address are displayed while creating it. Display "already taken" if entered ABHA address is already created by some other individual. Because no two ABHA address can be same.
12.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Create password, confirm password and click on "Submit" button. Password needs to be created as per password policy. Password policy:  8 characters or longer, one A-Z, one a-z, one 0-9, atleast one symbol, no space and not more than 2 consecutive characters or keyboard keys. | Check that adherence to password policy is must to create ABHA address. 
13.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Congratulation Screen is displayed stating "Congratulations! ABHA address name@abdm is created successfully " and click on "Login" button| Check that congratulations message is displayed after creating ABHA address & password. Also, an individual should be able to login with updated ABHA address and password.
14.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}|Click on "I Agree" against "Personal Data Processing Consent Form". Post this user is able to successfully login |	Check that when an individual login for first time, post agreeing to the "Personal Data Processing Consent Form" an individual is able to login.


## API Sequnce Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
autonumber
actor User
participant HIE-CM
note left of HIE-CM : ABHA number
User->>+HIE-CM: /api/v1/phr/registration/hid/search/auth-methods
HIE-CM-->>-User: Response: 200 OK 
note left of HIE-CM : authmethod, ABHA number
User->>+HIE-CM: /api/v1/phr/registration/hid/init/transaction
HIE-CM-->>-User: Response: 200 OK 
note right of User : Returns transactionId
note over User,HIE-CM : Resend OTP
note left of HIE-CM : transactionId
User->>+HIE-CM: /api/v1/phr/registration/hid/init/resendOtp
HIE-CM-->>-User: Response: 200 OK 
note right of User : Resends OTP
note right of User : Returns transactionId
note left of HIE-CM : transactionId,RSA Encrypted OTP
User->>+HIE-CM: /api/v1/phr/registration/hid/confirm/credential
HIE-CM-->>-User: Response: 200 OK 
note right of User : Returns transactionId,details of ABHA number
note left of HIE-CM : transactionId
User->>+HIE-CM: /api/v1/phr/registration/phr/suggestion
HIE-CM-->>-User: Response: 200 OK 
note right of User :Returns suggested phrAddresses 
note left of HIE-CM : PHRAddress
User->>+HIE-CM: /api/v1/phr/search/isExist
HIE-CM-->>-User: Response: 200 OK 
note right of User :Return PHR ADDRESS exist or not
note left of HIE-CM : transactionId,PHRAddress,RSA Encrypted password
User->>+HIE-CM: /api/v1/phr/registration/hid/create-phr-address
HIE-CM-->>-User: Response: 200 OK 
note right of User :Return user token id 
{{< /mermaid >}}

## API Information Request Response 

**Utilities**
- For encrypting the mobileNumber/AadharNumber/otp refer the [link](/abdm-docs/1-basics/encoding-rsa-encryption/#rsa-encryption)

  - To get public key for encryption refer the [link](/abdm-docs/1-basics/encoding-rsa-encryption/#api-to-retrieve-the-public-key)

- For converting an image into Base64 string refer the [link](/abdm-docs/1-basics/encoding-rsa-encryption/#convert-image-to-base64)


**1. Search a user by Health ID Number**

Api Checks Health ID Number to find user.

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/hid/search/auth-methods$" >}}


**2. Send OTP**

Api to create the transaction and send the otp on mobile number.

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/hid/init/transaction$" >}}

**3. Resend OTP**

API to resend the Mobile OTP

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/hid/init/resendOtp$" >}}

**4. Verify OTP**

API to verify OTP

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/hid/confirm/credential$" >}}

**5. Generate Suggestions**

API to Generate List phrAddresses as suggestions

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/phr/suggestion$" >}}

**6. Check PHR Address Already Exists**

API to check the PHR Address exist or not

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="GET /api/v1/phr/search/isExist$" >}}

**7. Create PHR Address**

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/hid/create-phr-address$" >}}

