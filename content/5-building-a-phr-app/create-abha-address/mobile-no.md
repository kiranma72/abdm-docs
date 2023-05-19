+++
title = "Using Mobile Number"
date = 2023-03-16T09:30:25+05:30
weight = 3
chapter = true
pre = "<b>5.1.1 </b>"
+++

# Using Mobile Number

|  Applicable To                             |   HMIS / LMIS (PVT)  |   Government Health App  |  
|-------------------------------|:----------------------:|:--------------------:|
|   Using Mobile Number                     |  {{% badge %}}Optional{{% /badge %}}       |  {{% badge %}}Optional{{% /badge %}}         | 

## Functionality Overview

**Description:** Individual enters mobile number/email ID, and it is validated via the added mode of validation

- Create an ABHA address of the format abc@abdm via mobile number / email ID using self-declared profile information filled in by an individual, such as photo, name, date of birth, gender, address. Mobile number is entered in profile info, in case a user is registering through mobile number and email ID is entered in profile info, in case a user is registering through email ID.
- Individual creates an easy to remember ABHA Address along with its password to login
- Profile is completed with an ABHA Address and a QR Code (with self-declared information filled in)
- This is a way of ABHA Address Registration with self-declared information

**ABHA Address Policy**

1. ABHA Address Policy:
	- Minimum length 4 including alphabet, number & dot(.) are allowed. Number cannot be in beginning and dot(.) cannot be in beginning & end.
	- As a policy we allow creation of all numeric Abha addresses for Abha Number only: 14digit@abdm.

2. 10-digit Mobile number as ABHA Address:
	- For now, we have restricted the creation of (10 digit) Mobile.No@ABDM

3. Creation of (14 digit@abdm):
	- ABHA Address is not allowed however we have the provision for the user to login with same 14digit@abdm both in web PHR and mobile PHR.

4. Password validation :
	- This has been made optional. You may kindly check the below APIs at your end and reach out to us in case of any issues:
		- Registration via ABHA:/api/v1/phr/registration/hid/create-phr-address
		- Registration via Mobile and Email: /api/v1/phr/registration/create/phr

## Test Cases

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

## API Sequnce Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
autonumber
actor User
participant HIE-CM
note right of User : RSA Encrypted mobile number/Email
User->>+HIE-CM: /api/v1/phr/registration/generate/otp
HIE-CM-->>-User: Response: 200 OK 
note right of User : Generate OTP on given mobile number/email
note right of User : Returns transactionId
note over User,HIE-CM : Resend OTP
note left of HIE-CM : transactionId
User->>+HIE-CM: /api/v1/phr/registration/resend/otp
HIE-CM-->>-User: Response: 200 OK 
note right of User : Resends OTP
note right of User : Returns transactionId
note left of HIE-CM : transactionId,RSA Encrypted OTP
User->>+HIE-CM: /api/v1/phr/registration/verify/otp
HIE-CM-->>-User: Response: 200 OK 
note right of User : Returns transactionId,mapped PHR Address
note left of HIE-CM: Beneficiary data
User->>+HIE-CM: /api/v1/phr/registration/details
HIE-CM-->>-User: Response: 200 OK 
note right of User : Returns transactionId
note left of HIE-CM : transactionId
User->>+HIE-CM: /api/v1/phr/registration/phr/suggestion
HIE-CM-->>-User: Response: 200 OK 
note right of User :Returns suggested phrAddresses 
note left of HIE-CM : PHRAddress
User->>+HIE-CM: /api/v1/phr/search/isExist
HIE-CM-->>-User: Response: 200 OK 
note right of User :Return PHR ADDRESS exist or not
note left of HIE-CM : transactionId,PHRAddress,RSA Encrypted password
User->>+HIE-CM: /api/v1/phr/registration/create/phr 
HIE-CM-->>-User: Response: 200 OK 
note right of User :Returns user token id 
{{< /mermaid >}}

## API Information Request Response 

**Utilities**
- For encrypting the mobileNumber/AadharNumber/otp refer the [link](/abdm-docs/1-basics/encoding-rsa-encryption/#rsa-encryption)

  - To get public key for encrypting refer the [link](/abdm-docs/1-basics/encoding-rsa-encryption/#api-to-retrieve-the-public-key)

- For converting an image into Base64 string refer the [link](/abdm-docs/1-basics/encoding-rsa-encryption/#convert-image-to-base64)


**1. Generate OTP**

Api Accepts Mobile Number/Email and then Generates OTP for it.

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /v1/phr/registration/generate/otp$" >}}


**2. Resend OTP**

Api Accepts Transaction Number and then Resend OTP for it.

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /v1/phr/registration/resend/otp$" >}}

**3. Validate OTP**

API to verify the Mobile OTP

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /v1/phr/registration/verify/otp$" >}}

**4. Pass the Beneficiary Details**

API to Pass the Beneficiary Details so based on the details suggestions of PHR Addresses can be obtained

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /v1/phr/registration/details$" >}}

**5. Generate Suggestions**

API to Generate List phrAddresses as suggestions

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /v1/phr/registration/phr/suggestion$" >}}

**6. Check PHR Address Already Exists**

API to check the PHR Address exist or not

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="GET /v1/phr/search/isExist$" >}}

**7. Register the Beneficiary**

Register the Beneficiary to the PHR using the Mobile/Email Address

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /v1/phr/registration/create/phr$" >}}
