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

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with mobile number flow|Enter mobile number linked with ABHA address||
2.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with mobile number flow|Validate mobile number via mobile OTP  | Check if an individual receives mobile OTP and able to login with mobile number
3.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with mobile number flow|Resend Mobile OTP after 60 seconds post clicking on "Resend OTP". ||
4.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with mobile number flow|Display ABHA addresses linked with entered validated mobile number. So that an individul can select an ABHA address in which one wishes to login.  ||
5.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with e-mail ID flow | Enter e-mail ID linked with ABHA address
6.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with e-mail ID flow | Validate e-mail ID via e-mail OTP|Check if an individual receive email OTP and login with e-mail OTP
7.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with e-mail ID flow| Resend e-mail OTP after 60 seconds post clicking on "Resend OTP|Check if an individual receive email OTP after 60 seconds  and login with e-mail OTP
8.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with e-mail ID flow | Display ABHA addresses linked with entered validated e-mail ID. So that an individul can select an ABHA address in which one wishes to login.|Check if all ABHA addresses linked with entered email ID are displayed and an individual is able to login in selected ABHA address
9.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with easy to remember ABHA address (name@abdm) flow|Enter easy to remember ABHA address - name@abdm||
10.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with easy to remember ABHA address (name@abdm) flow|Validate ABHA address via password / mobile OTP / e-mail OTP / aadhar OTP as per auth mode|Check if an individual is able to login with easy to remember ABHA address via password
11.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with easy to remember ABHA address (name@abdm) flow|Validate ABHA address via password / mobile OTP / e-mail OTP / aadhar OTP as per auth mode|Check if an individual is able to login with easy to remember ABHA address via mobile OTP / e-mail OTP / aadhar OTP as per auth mode
12.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with easy to remember ABHA address (name@abdm) flow|Resend aadhar OTP / mobile OTP / e-mail OTP after clicking on "Resend OTP|Check if an individual receive aadhar OTP / mobile OTP/e-mail OTP after 60 seconds and an individual is able to login post validation of ABHA address
13.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with default ABHA address (14-digit@abdm) flow|Enter default ABHA address such as 14-digit@abdm||
14.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with default ABHA address (14-digit@abdm) flow|Validate ABHA address via mobile OTP / aadhar OTP | Check if aadhar OTP / mobile OTP is received and post validation of ABHA number, an individual is able to successfully login 
15.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Login with default ABHA address (14-digit@abdm) flow|Resend aadhar OTP / mobile OTP after clicking on "Resend OTP" | Check if an individual receive aadhar OTP / mobile OTP after 60 seconds and an individual is able to login post validation of ABHA address
16.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with ABHA number flow|Enter 14 digit ABHA number||
17.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with ABHA number flow|Validate ABHA number via aadhar OTP / mobile OTP | Check if aadhar OTP / mobile OTP is received and post validation of ABHA number, an individual is able to successfully login 
18.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Login with ABHA number flow| Resend aadhar OTP / mobile OTP after clicking on "Resend OTP| Check if an individual receive aadhar OTP / mobile OTP after 60 seconds and an individual is able to login post validation of ABHA number
19.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Reset Password|Login with any mode - mobile number / email ID / default ABHA address / easy to remember ABHA address / ABHA number|Check if password can be updated by an individual post login with any mode
20.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Reset Password|Post successful login, click on reset password withing setting of the menu bar||
21.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Reset Password|Create password as per password policy. Password policy: 8 characters or longer, one A-Z, one a-z, one 0-9, atleast one symbol, no space and not more than 2 consecutive characters or keyboard keys. | Check if password is created as per password policy
22.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Reset Password|Confirm password  | Check new password is created only after same password is confirmed again
23.|{{% badge style="blue"  %}}Mandatory{{% /badge %}} Reset Password|A message is displayed called "Your password is successfully changed" | Check if an individual new password is created by login with new password


## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Login to PHR App using ABHA Address
PHR App->>HIE-CM:GET /v1/apps/phrAddres/search/auth-mode
note left of HIE-CM: Select any Auth Mode
PHR App->>HIE-CM:POST /v1/apps/phrAddres/auth-init
PHR App->>HIE-CM:POST /v1/apps/phrAddres/auth-confirm
{{< /mermaid >}}

---

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Login to PHR App using Mobile number/Email
PHR App->>HIE-CM:POST /v1/apps/login/mobileEmail/auth-init
PHR App->>HIE-CM:Verify mobile number/email<br/>POST /v1/apps/login/mobileEmail/pre-Verify
PHR App->>HIE-CM:POST /v1/apps/login/mobileEmail/auth-confirm
{{< /mermaid >}}

---

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Login to PHR App using ABHA number
PHR App->>HIE-CM:POST /v1/apps/login/hid/search/auth-mode
PHR App->>HIE-CM:POST /v1/apps/login/hid/auth-init
PHR App->>HIE-CM:POST /v1/apps/login/mobileEmail/pre-Verify
PHR App->>HIE-CM:POST /v1/apps/login/mobileEmail/auth-confirm
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



