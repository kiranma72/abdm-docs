+++
title = "Login & Manager User"
date = 2023-04-24T05:53:25+05:30
weight = 2
chapter = true
pre = "<b>5.2 </b>"
+++

# Login & Manager User Profiles

## Functionality Overview

- PHR App should **allow the user to log in to the PHR application** with any of the Auth methods.

- It can also save the refresh token and extend the user session to reduce the number of times the user has to keep logging in.

- A single PHR app can manage multiple user profiles by offering a sign in-sign out

- *More information:*
Every PHR Applicationi user needs to have an ABHA Address (also reffered to as PHR Address). The address looks like "username@hie-cm". Currently ABDM manages 2 HIE-CMs. The Sandbox HIE-CM @sbx and the production HIE-CM @abdm. PHR Apps use APIs provided by the HIE-CM to create a new ABHA address for users. 
The user chosen ABHA address has to be alphanumeric. The only numeric address allowed is 14 digits and that must be a valid ABHA number. 

**Manage Profile:**

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

**1. Get Authentication Methods**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="GET /v1/apps/phrAddress/search/auth-mode$" >}}


**2. Initiate Login Transaction**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/phrAddress/auth-init$" >}}


**3. Verify Login Transaction**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/phrAddress/auth-confirm$" >}}



