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


## API Sequence Diagram

[![](https://mermaid.ink/img/pako:eNp9kLFOwzAQhl_l5IUlVQY2D5VSKshSURpYkJcjvhBLzjnYl0JU9d1xW7ogxHb6df93p--g2mBJaZXoYyJuae3wPeJgWJx4gqZFhpdE8SZBtaoreNrBXW6ABNhTdN18iStrI6VkGFsJ8dwwXO-2i-XyNOua0EsP99g672SGlLnpN_j0iuFqtd5Ag2zfwhc8oNAnzhmTYXr72DyX-9uyd2M5ojhiKccYOuepTD1Gut78i_FvO_DiDFCFGigO6Gx2cjAMYJT0NJBROo-WOpy8GGX4mFdxktDM3CotcaJCTaPNt34UKt2hTzkl67KTzcXzWXehRuTXEK47x2_LlIZo?type=png)](https://mermaid.live/edit#pako:eNp9kLFOwzAQhl_l5IUlVQY2D5VSKshSURpYkJcjvhBLzjnYl0JU9d1xW7ogxHb6df93p--g2mBJaZXoYyJuae3wPeJgWJx4gqZFhpdE8SZBtaoreNrBXW6ABNhTdN18iStrI6VkGFsJ8dwwXO-2i-XyNOua0EsP99g672SGlLnpN_j0iuFqtd5Ag2zfwhc8oNAnzhmTYXr72DyX-9uyd2M5ojhiKccYOuepTD1Gut78i_FvO_DiDFCFGigO6Gx2cjAMYJT0NJBROo-WOpy8GGX4mFdxktDM3CotcaJCTaPNt34UKt2hTzkl67KTzcXzWXehRuTXEK47x2_LlIZo)


## Test Cases:

Applicable | Test Title | Test Summary | Optional or Mandatory | Test Scenario | API Sequence | Expected Result | Actual Result
| ------| ----------- | ----------- | ----- | ------------------- | ------- | --------- | --------- |
Sample|Sample|Sample|Sample|Sample|Sample|Sample|Sample|


