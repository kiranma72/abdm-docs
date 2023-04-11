+++
title = "Using Mobile Number"
date = 2023-03-16T09:30:25+05:30
weight = 3
chapter = true
pre = "<b>4.2.1 </b>"
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

*check with Kiran*

Functionality|Test Case|Steps To Be Executed|
| ----- | ----- | ----- |
{{% badge style="blue" %}}Mandatory{{% /badge %}} add |add |add

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

**1. Generate OTP**

Api Accepts Mobile Number/Email and then Generates OTP for it.

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/generate/otp$" >}}


**2. Resend OTP**

Api Accepts Transaction Number and then Resend OTP for it.

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/resend/otp$" >}}

**3. Validate OTP**

API to verify the Mobile OTP

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/verify/otp$" >}}

**4. Pass the Beneficiary Details**

API to Pass the Beneficiary Details so based on the details suggestions of PHR Addresses can be obtained

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/details$" >}}

**5. Generate Suggestions**

API to Generate List phrAddresses as suggestions

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/phr/suggestion$" >}}

**6. Check PHR Address Already Exists**

API to check the PHR Address exist or not

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="GET /api/v1/phr/search/isExist$" >}}

**7. Register the Beneficiary**

Register the Beneficiary to the PHR using the Mobile/Email Address

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/create/phr$" >}}
