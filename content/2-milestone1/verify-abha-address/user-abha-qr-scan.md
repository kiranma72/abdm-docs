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

[![](https://mermaid.ink/img/pako:eNp1UU1PAjEQ_SuTXrzsBqK3HkgWiXIhIqsX08vYDtC4O13bLroh_He7iyRK4Dadvq_M2wvtDAkpAn22xJpmFjcea8XRxoqg1MjwGsjfBCim8wKeV3CfGBAd7MjbdXdcF8Z4CkEx6uj8wFA8Xy3zyaSf5Zywilt4QG0rGzsISTecC_dRTqxiOltAiWze3Tc8YqQv7OTyqXwZ7e5G0X0QjzbE5NNPPjwVX6LkSSoJyhWFxnEguB2PryCPwP8WjvNzlz7etXx_XUQmavI1WpOuu1cMoETcUk1KyDQaWmNbRSUUHxIU2-jKjrWQ0beUibYxSfO3DCHXWIW0JWPTdRfHxobiMtEgvzl3whx-AC5NniA?type=png)](https://mermaid.live/edit#pako:eNp1UU1PAjEQ_SuTXrzsBqK3HkgWiXIhIqsX08vYDtC4O13bLroh_He7iyRK4Dadvq_M2wvtDAkpAn22xJpmFjcea8XRxoqg1MjwGsjfBCim8wKeV3CfGBAd7MjbdXdcF8Z4CkEx6uj8wFA8Xy3zyaSf5Zywilt4QG0rGzsISTecC_dRTqxiOltAiWze3Tc8YqQv7OTyqXwZ7e5G0X0QjzbE5NNPPjwVX6LkSSoJyhWFxnEguB2PryCPwP8WjvNzlz7etXx_XUQmavI1WpOuu1cMoETcUk1KyDQaWmNbRSUUHxIU2-jKjrWQ0beUibYxSfO3DCHXWIW0JWPTdRfHxobiMtEgvzl3whx-AC5NniA)


## Test Cases:

Applicable | Test Title | Test Summary | Optional or Mandatory | Test Scenario | API Sequence | Expected Result | Actual Result
| ---| ----------- | --------------- | --- | ------------------- | ------- | ------------- | --------- |
All|VRFY_ABHA_501 - Reading ABHA Profile Info using ABHA QR Code|System must allow scanning of ABHA QR code to read the ABHA information|Optional|EMR/HMIS scans the user's ABHA QR code|**No content??**|System reads the user information from the ABHA QR code - name, date of birth, gender, mobile and other details into the system for registration.|**No content??**|


