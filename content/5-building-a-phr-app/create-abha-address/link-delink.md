+++
title = "Link/De-link ABHA Address"
date = 2023-03-30T09:30:25+05:30
weight = 5
chapter = true
pre = "<b>5.1.3 </b>"
+++

# Link and De-Link ABHA Address

## Functionality Overview 

- ABDM has now segregated the identity layer from the consent layer, which will ensure that the ABHA Number (earlier known as Health ID) provides a strong identity   to an individual whereas an ABHA Address (earlier known as PHR Address) enables an individual to share their health records with different healthcare providers and payers.
- API links the given ABHA Address to the ABHA number and defines whether it is the preferred ABHA Address
- An **ABHA address can be created without KYC,** using just the mobile number, name, YoB, gender.
- Users can have more than 1 ABHA address. ABDM encourages Users to have just 1 ABHA address.
- Users can have only a unique KYC-verified ABHA number.
- There are several **scenarios where a strong KYC may be required** (example: Insurance) for your ABHA address. This is achieved by linking your ABHA address with your ABHA number.
- Alternatively, several people who use public health facilities may be issued an ABHA number as part of the process.
- They can create an ABHA address and link it to their ABHA number.
- Remember that the ABHA number acts as an ABHA Address like “14digit@abdm”


**Step 1:** User must create an ABHA number, [using Aadhar or driving license.](/abdm-docs/2-milestone1/abha-number/index.html)

**Step 2:** Users can link an existing ABHA address to this ABHA number, OR you can create and link a new ABHA address

**Step 3:** Users can unlink an ABHA number from an ABHA address


## Test Cases

S.No.|Functionality|Test Case|Steps To Be Executed|
| --| ----- | ----- | ----- |
1|{{% badge style="blue" %}}Mandatory{{% /badge %}} Linking of ABHA Number and ABHA Address (LINK_ABHA_701)|System should have provision to link the  created ABHA  number with existing ABHA address |**1.** User will create ABHA  number as deifned in above scenerios. **2.** user should be able to link ABHA  number with existing ABHA address 

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


## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Link/Delink ABHA Address & ABHA number
actor User
User->>HIE-CM: POST /v1/phr/registration/hid/search/auth-methods
User->>HIE-CM: POST /v1/phr/login/init/transaction
User->>HIE-CM: POST /v1/phr/registration/hid/init/resendOtp
User->>HIE-CM: POST /v1/phr/login/mobileEmail/preVerification
note over HIE-CM,User: Link ABHA Address & ABHA Number
User->>HIE-CM: POST /v1/phr/profile/link/hid
note over HIE-CM,User: Delink ABHA Address & ABHA Number
User->>HIE-CM: POST /v1/phr/profile/link/hid
{{< /mermaid >}}



## API Information Request Response 

**Utilities**
- For encrypting the mobileNumber/AadharNumber/otp refer the [link](/abdm-docs/8-utilities/utilities/#rsa-encryption)

  - To get public key for encrypting refer the [link](/abdm-docs/8-utilities/utilities/#api-to-retrieve-the-public-key)

- For converting an image into Base64 string refer the [link](/abdm-docs/8-utilities/utilities/#convert-image-to-base64)


Links the given ABHA Address to the ABHA number


## API Information Request Response 

**1. Search a user by Health ID Number**

Api Checks Health ID Number to find User.

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/hid/search/auth-methods$" >}}


**2. Generate OTP**

Api to create the transaction and send the otp on mobile number.

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/login/init/transaction$" >}}

**3. Resend OTP**

API to resend the Mobile OTP

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/registration/hid/init/resendOtp$" >}}

**4. Verify OTP**

API to verify OTP

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/login/mobileEmail/preVerification$" >}}

**5. Link the ABHA Address with ABHA Number**
API links the given ABHA Address with the ABHA number.

Refer to example “Link”

**BASE URL:** https://phrsbx.abdm.gov.in

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/profile/link/hid$" >}}


## De-Link the ABHA address with ABHA Number

API de-links the given ABHA Address from the ABHA number.

Refer to example “Delink”

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-updated.yml" api="POST /api/v1/phr/profile/link/hid$" >}}

