+++
title = "Manage User Profile"
date = 2023-04-24T05:53:25+05:30
weight = 3
chapter = true
pre = "<b>5.3 </b>"
+++

# Manage PHR App User's Profile

## Functionality Overview

- PHR applications need to have a (this) section, where **users can view their demographic details and update (edit) their information.**

- The section should also display ABHA QR code as part of the Profile information

- They should also be able to set/change password from this section.

- Similarly, they should also have an option to set/change consent pin.

- The user should also be able to upload a profile photo from this section.

## Test Cases

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

**Edit Profile** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for KYC verified profiles |Update mobile number| Mobile OTP is received on updated mobile no. Post mobile OTP validation, mobile no is updated. 
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for KYC verified profiles |Update email ID| E-mail OTP is received on updated e-mail ID. Post e-mail OTP validation, e-mail ID is updated. 
3| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for KYC verified profiles |Update address| All fields of address such as address line 1, district, state and pin-code can be updated. 
4| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update Photo|Photo can be edited by an individul taking the picture from mobile camera / upload photo from gallery of the device 
5| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update Full Name| Update First Name, Middle name and Last Name
6| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update Gender | Update Gender
7| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update DoB| Update Day, Month and Year
8| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update Mobile No| Mobile OTP is received on updated mobile no. Post mobile OTP validation, mobile no is updated.
9| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update Email ID| E-mail OTP is received on updated e-mail ID. Post e-mail OTP validation, e-mail ID is updated.  
10| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit profile for Self-Declared profile |Update Address| All fields of address such as address line 1, district, state and pin-code can be updated. 


## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Manager User Profiles with PHR App
note over PHR App,HIE-CM: Get User Profile
PHR App->>HIE-CM:GET /v1/apps/profile/me
note over PHR App,HIE-CM: Update Profile
PHR App->>HIE-CM:POST v1/apps/profile/update
note over PHR App,HIE-CM: Reset Password
PHR App->>HIE-CM:/v1/apps/patients/profile/reset-password
note over PHR App,HIE-CM: Get patient QR Code
PHR App->>HIE-CM:GET /v1/apps/patients/qr-code
note over PHR App,HIE-CM: Create Consent Pin
PHR App->>HIE-CM:POST /patients/pin
note over PHR App,HIE-CM: Reset Consent Pin
PHR App->>HIE-CM:POST /patients/verify-pin
PHR App->>HIE-CM:POST /patients/change-pin
note over PHR App,HIE-CM: Forgot Consent Pin
PHR App->>HIE-CM:POST /patients/forgot-pin/generate-otp
PHR App->>HIE-CM:POST /patients/forgot-pin/validate-otp
PHR App->>HIE-CM:POST /patients/reset-pin
{{< /mermaid >}}


## API Information Request Response

{{% notice title="Manage User Profiles" %}}

  - [Profile Collection API](#profile-collection-api)
  - [Manage Consent Pin](#manage-consent-pin)

{{% /notice %}}

**Utilities**
- For encrypting the mobileNumber/AadharNumber/otp refer the [link](/abdm-docs/8-utilities/utilities/#rsa-encryption)

  - To get public key for encrypting refer the [link](/abdm-docs/8-utilities/utilities/#api-to-retrieve-the-public-key)

- For converting an image into Base64 string refer the [link](/abdm-docs/8-utilities/utilities/#convert-image-to-base64)

#### Profile Collection API

**1. Get User Details**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="GET /v1/apps/profile/me$" >}}

**2. Update User Profile Details**

**BASE URLs:**  https://dev.abdm.gov.in/cm

-- YET TO ADD --

**2. Reset Password**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/patients/profile/reset-password$" >}}


**3. Get Patient's QR Code**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="GET /v1/apps/patients/qr-code$" >}}

#### Manage Consent Pin


**4. Create Transaction Pin**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /patients/pin$" >}}

**5. Verify Pin**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /patients/verify-pin$" >}}

**6. Change Pin**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /patients/change-pin$" >}}

**7. Generate OTP For Forgot Pin**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /patients/forgot-pin/generate-otp$" >}}

**8. Validate OTP For Forgot Pin**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /patients/forgot-pin/validate-otp$" >}}

**9. Reset Pin**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="PUT /patients/reset-pin$" >}}








