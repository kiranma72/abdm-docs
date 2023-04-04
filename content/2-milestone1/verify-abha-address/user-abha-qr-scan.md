+++
title = "Scan User ABHA QR"
date = 2023-03-16T09:30:25+05:30
weight = 2
chapter = true
pre = "<b>2.3.2 </b>"
+++

# Scan User ABHA QR
|  Applicable To                             |   HMIS / LMIS (PVT)  |   Government Health App  |     PHR / LOCKER    |
|-------------------------------|:----------------------:|:--------------------:|:-------------------:|
|   Scan User ABHA QR                      |  {{% badge style="blue" %}} Mandatory{{% /badge %}}       |  {{% badge style="blue" %}} Mandatory{{% /badge %}}        |  {{% badge color="red"%}}Not Applicable{{% /badge %}}     |


## Functionality Overview

Health Facility can scan the **User's ABHA QR code**, whereby User provides consent to link the Health Record to their account.

Health Facility (HIP) Initiated linking is the process through which an HIP links the patient’s care context (health record) with the patient ABHA Address, after patient registration and creation of health records (in their HMIS/LMIS system).

**Sample QR Codes**

QR Code|JSON output
| -------- | ------- |
Sample QR Code in User's ABHA Application ![ABHA App QR Code](../abha-qr-in-app.png) | ![ABHA App QR Scan](../json-abha-app-qr-scan.png)
Sample QR Code in User's ABHA Card ![ABHA App QR Code](../abha-card-eg.png) | ![ABHA App QR Scan](../json-abha-card-qr.png)

Care context (Health record) linking happens in two steps:

1. Link token generation
2. Linking care context with ABHA address after obtaining valid link token

**Link Token generation**

To achieve linking, the Health Facility (HIP) needs to have a valid link token. There are two possible ways to get the link token:
1. Through scan and share profile use case
2. Using link token service

The link token will be used for linking multiple number of care contexts, and concurrent linkages.

**Pre-requisites:**
1. Patient must have a ABHA app with a valid ABHA address or physical card like a ABHA card
2. Hospital must have a 2D Barcode scanner available at the registration counter.
	- The HRP software registration page have text box to load data scanned from ABHA QR Code.

**Steps to scan User's ABHA QR Code**

1. Hospital operator scans the QR code on patient ABHA card or as displayed in ABHA mobile App
	- The Patient details like ABHA address, Name, DOB, Gender, State Id, District Id, etc are embedded in the QR code as a JSON
2. HRP software must validate the scanned data and collect a Linking Token from ABDM Gateway
3. The software must use the information scanned to register the patient and save the ABHA Address

## Sample User Experience

Here's how the user journey looks on the Health Facility's side:

![Scan User ABHA QR Code](/abdm-docs/img/scan-user-qr.gif)


## Test Cases:

S.no.|Applicable To | Test Summary | Test Scenario |
|--| --| ----------- | ------------------- |
1.|{{% badge %}}Optional{{% /badge %}} Applicable to All (VRFY_ABHA_501)| System must allow scanning of ABHA QR code to read the user's ABHA information|EMR/HMIS scans the user's ABHA QR code


## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Scan User's ABHA QR Code to verify ABHA Address
actor User
HRP->>User:Health Facility scans User's ABHA QR code
HRP->>ABDM Sandbox Gateway:POST/v3/token/generate-token
ABDM Sandbox Gateway-->>HRP:Response 200
ABDM Sandbox Gateway->>HRP:POST/v3/token/on-generate-token
HRP-->>ABDM Sandbox Gateway:Response 200
{{< /mermaid >}}


## API Information Request Response 

**1. Generate link token**

**BASE URLs:**
  - Sandbox Server URL: https://dev.abdm.gov.in/hiecm/api/

  - Production Server URL: https://live.abdm.gov.in/hiecm/api

{{< swaggermin src="/abdm-docs/Yaml/HIECM-LinkTokenService.yml" api="POST /v3/token/generate-token" >}}

**2. Call back API**

**BASE URLs:**
  - Sandbox Server URL: https://dev.abdm.gov.in/hiecm/api/

  - Production Server URL: https://live.abdm.gov.in/hiecm/api

{{< swaggermin src="/abdm-docs/Yaml/HIECM-LinkTokenService.yml" api="POST /{callback_url}/v3/hip/token/on-generate-token$" >}}

## Verify ABHA Address by demographic

If Linking token has expired (more than 6 months old or it has been already used once). In that case, all the demographic information is available and can be used directly.