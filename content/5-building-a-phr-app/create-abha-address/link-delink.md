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
- ABHA number can be linked or de-linked with the ABHA address. 
- API links the given ABHA Address to the ABHA number and defines whether it is the preferred ABHA Address

## Test Cases

Functionality|Test Case|Steps To Be Executed|
| ----- | ----- | ----- |
{{% badge style="blue" %}}Mandatory{{% /badge %}} Linking of ABHA Number and ABHA Address (LINK_ABHA_701)|System should have provision to link the  created ABHA  number with existing ABHA address |**1.** User will create ABHA  number as deifned in above scenerios. **2.** user should be able to link ABHA  number with existing ABHA address 

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
- For encrypting the mobileNumber/AadharNumber/otp refer the [link](/abdm-docs/1-basics/encoding-rsa-encryption/#rsa-encryption)

  - To get public key for encrypting refer the [link](/abdm-docs/1-basics/encoding-rsa-encryption/#api-to-retrieve-the-public-key)

- For converting an image into Base64 string refer the [link](/abdm-docs/1-basics/encoding-rsa-encryption/#convert-image-to-base64)


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

