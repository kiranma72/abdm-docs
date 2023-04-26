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

**1. Get Authentication Methods**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="GET /v1/apps/phrAddress/search/auth-mode$" >}}


**2. Initiate Login Transaction**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/phrAddress/auth-init$" >}}


**3. Verify Login Transaction**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/phrAddress/auth-confirm$" >}}



