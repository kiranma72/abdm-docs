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

|      Applicable To                         |   HMIS / LMIS (PVT)  |   Government Health App  |   PHR / LOCKER    |
|-------------------------------|----------------------|--------------------|-------------------|
|   **2.1 Creation of ABHA Number**            |                      |                    |                   |
|   2.1.1 Using Aadhar OTP                      |   Mandatory          |   Mandatory        |   Mandatory       |
|   2.1.2 Using Aadhar Biometrics                      |   Optional           |   Mandatory        |   Optional        |
|   2.1.3 Using Aadhar Demographics (OFFLINE)                     |   Not Applicable     |   Mandatory        |   Not Applicable  |
|   2.1.4 Using Driving License              |   Optional           |   Optional         |   Optional        |
|   **2.2 Creation of ABHA Address**       |                      |                    |                   |
|   2.2.1 Using Mobile Number               |   Optional           |   Optional         |   Mandatory       |
|   2.2.2 Using ABHA Number                  |   Optional           |   Optional         |   Mandatory       |
|   **2.3 Verification of ABHA Address**   |                      |                    |                   |
|   2.3.1 Scan Health Facility QR      |   Mandatory          |   Mandatory        |   Mandatory       |
|   2.3.2 Scan User ABHA QR          |   Mandatory          |   Mandatory        |   Not Applicable  |
|   2.3.3 By OTP             |   Mandatory          |   Mandatory        |   Not Applicable  |
|   2.3.4 New vs Returning Patients  |   Mandatory          |   Mandatory        |   Not Applicable  |

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
