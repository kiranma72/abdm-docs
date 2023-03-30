+++
title = "Milestone 1"
date = 2023-03-16T04:10:00+05:30
weight = 2
chapter = true
pre = "<b>2. </b>"
+++

## Get Milestone 1 Certified

Functionalities offered by Milestone 1 are:
1. Create ABHA number & address - using Aadhaar / Mobile / Driving License
2. Collect & Verify ABHA address during patient registration


## M1 Testcases mapping by Role

|                               |   HMIS / LMIS (PVT)  |   Government Health App  |   PHR / LOCKER    |
|-------------------------------|----------------------|--------------------|-------------------|
|   **2.1 Creation of ABHA Number**            |                      |                    |                   |
|   2.1.1 Using Aadhar OTP                      |   Mandatory          |   Mandatory        |   Mandatory       |
|   Using Aadhar Demographics (OFFLINE)                     |   Not Applicable     |   Mandatory        |   Not Applicable  |
|   Using Aadhar Biometrics                      |   Optional           |   Mandatory        |   Optional        |
|   Using Driving License              |   Optional           |   Optional         |   Optional        |
|   **Creation of ABHA Address**       |                      |                    |                   |
|   Using Mobile Number               |   Optional           |   Optional         |   Mandatory       |
|   Using ABHA Number                  |   Optional           |   Optional         |   Mandatory       |
|   **Verification of ABHA Address**   |                      |                    |                   |
|   Scan Health Facility QR Code     |   Mandatory          |   Mandatory        |   Mandatory       |
|   Scan User ABHA QR Code          |   Mandatory          |   Mandatory        |   Not Applicable  |
|   By OTP             |   Mandatory          |   Mandatory        |   Not Applicable  |
|   New vs Returning Patients  |   Mandatory          |   Mandatory        |   Not Applicable  |

This section covers:
{{% notice %}}
- Creation of ABHA number
	- Using Aadhaar OTP
	- Using Aadhaar biometric
	- Using Aadhaar demographic(offline mode)
	- Using driving license
- Creation of ABHA address
	- Using mobile number
	- Using ABHA number
- Verification of ABHA address
	- By scan & share
	- By OTP
	- By demographic 
{{% /notice %}}
