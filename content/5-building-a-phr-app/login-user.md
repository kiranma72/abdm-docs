+++
title = "Login to PHR App"
date = 2023-04-24T05:53:25+05:30
weight = 2
chapter = true
pre = "<b>5.2 </b>"
+++

# Login to PHR App

## Functionality Overview

- PHR App should **allow the user to log in to the PHR application** with any of the Auth methods.

- It can also save the refresh token and extend the user session to reduce the number of times the user has to keep logging in.

- A single PHR app can manage multiple user profiles by offering a sign in-sign out

- *More information:*
Every PHR Applicationi user needs to have an ABHA Address (also reffered to as PHR Address). The address looks like "username@hie-cm". Currently ABDM manages 2 HIE-CMs. The Sandbox HIE-CM @sbx and the production HIE-CM @abdm. PHR Apps use APIs provided by the HIE-CM to create a new ABHA address for users. 
The user chosen ABHA address has to be alphanumeric. The only numeric address allowed is 14 digits and that must be a valid ABHA number. 

![Different Login Methods](../different_login_methods.png)

To Use Login APIs (PHR id is required under request body), the user need to setup his/her own PHR id
![Creating PHR ID](../creating_phr_id.png)


## Test Cases

Check with Rachna and Team


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
{{% notice title="Different Methods Of Login" %}}

  - [Login Using ABHA Address](#login-using-abha-address)
  - [Login Using Mobile Number/Email](#login-using-mobile-numberemail)
  - [Login Using ABHA Number](#login-using-abha-number)

{{% /notice %}}

**Utilities**
- For encrypting the mobileNumber/AadharNumber/otp refer the [link](/abdm-docs/8-utilities/utilities/#rsa-encryption)

  - To get public key for encrypting refer the [link](/abdm-docs/8-utilities/utilities/#api-to-retrieve-the-public-key)

- For converting an image into Base64 string refer the [link](/abdm-docs/8-utilities/utilities/#convert-image-to-base64)

#### Login Using ABHA Address

**1. Initiate Login Transaction**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/phrAddress/auth-init$" >}}

**2. Verify Login Transaction**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/phrAddress/auth-confirm$" >}}

#### Login Using Mobile Number/Email

**3. Generate Mobile/Email OTP**

Generate Mobile/Email OTP to start Login transaction

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/login/mobileEmail/auth-init$" >}}

**4. Verify Mobile/Email OTP**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/login/mobileEmail/pre-Verify$" >}}

**5. Get User Token**

Get the User Token in the mobile/email login flow

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/login/mobileEmail/auth-confirm$" >}}

#### Login Using ABHA Number

**6. Search User by Health ID Number**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/login/hid/search/auth-mode$" >}}

**7. Initiate Login Transaction Using HealthId Number**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/login/hid/auth-init$" >}}

**8. Verify Mobile OTP**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/login/mobileEmail/pre-Verify$" >}}

**9. Get the User Token**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/login/mobileEmail/auth-confirm$" >}}



