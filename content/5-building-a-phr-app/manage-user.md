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


## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Login & Manager User Profiles with PHR App
PHR App->>HIE-CM:GET /v1/apps/phrAddres/search/auth-mode
note left of HIE-CM: Select any Auth Mode
HIE-CM->>PHR App:POST /v1/apps/phrAddres/auth-init
PHR App->>HIE-CM:POST /v1/apps/phrAddres/auth-confirm
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








