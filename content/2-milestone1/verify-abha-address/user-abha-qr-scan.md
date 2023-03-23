+++
title = "By Scanning User ABHA QR Code"
date = 2023-03-16T09:30:25+05:30
weight = 2
chapter = true
pre = "<b>2.3.2 </b>"
+++

# By Scanning User ABHA QR Code

## Functionality Overview

Health Facility can scan the **User's ABHA QR code**, whereby User provides consent to link the Health Record to their account.

Health Facility (HIP) Initiated linking is the process through which an HIP links the patient’s care context (health record) with the patient ABHA Address, after patient registration and creation of health records (in their HMIS/LMIS system).

## Sample QR Codes

1. QR Code in User's ABHA Application

![PHR App QR Code](../phrqr-in-app.png)

2. QR Code in User's ABHA Card

![ABHA card example](../abha-card-eg.png)

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


## Test Cases:

Applicable | Test Title | Test Summary | Optional or Mandatory | Test Scenario | API Sequence | Expected Result | Actual Result
| ---| ----------- | --------------- | --- | ------------------- | ------- | ------------- | --------- |
All|VRFY_ABHA_501 - Reading ABHA Profile Info using ABHA QR Code|System must allow scanning of ABHA QR code to read the ABHA information|Optional|EMR/HMIS scans the user's ABHA QR code|v3/token/generate-token, v3/token/on-generate-token|System reads the user information from the ABHA QR code - name, date of birth, gender, mobile and other details into the system for registration.|**No content??**|

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

{{< swaggermin src="/abdm-docs/Yaml/HIECM-LinkTokenService.yml" api="POST /v3/token/generate-token$" >}}

**2. Call back API**

{{< swaggermin src="/abdm-docs/Yaml/HIECM-LinkTokenService.yml" api="POST /{callback_url}/v3/hip/token/on-generate-token$" >}}

