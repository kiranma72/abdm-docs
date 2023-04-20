+++
title = "Milestone 2"
date = 2023-04-03T04:10:00+05:30
weight = 3
chapter = true
pre = "<b>3. </b>"
+++

## Get Milestone 2 Certified

**Functionalities of Milestone 2:** Building Health Information Provider (HIP) services to share digital records via any Personal Health Records (PHR) application.

The Milestone 2 can be explained with 2 scenarios:

**Scenario 1:**
- User has shared ABHA Address during Registration (1 of 3 ways from [verification of ABHA address](/abdm-docs/2-milestone1/verify-abha-address/index.html))
- Expectation is HIP initiated linking (that whenever a new health record is created for this user, it is linked to a care context)

**Scenario 2:**
- User has not shared ABHA Address during Registration.
- Expectation is to send an SMS that a new health record is available with a deep link; and to support user initiated discovery & linking

Milestone 2 revolves around HRPs, here's a quick snapshot to understand what functionalities will be covered in this section:

![HRP Milestone 2 Functionalities](/abdm-docs/img/hrp-milestone2.jpg) 


## M2 Test Cases mapping by Role

|      Applicable To                         |   HMIS / LMIS (PVT)  |   Govt. Health App  |   
|-------------------------------|----------------------|--------------------|                 
|   **Health Record Formats**                      |   Mandatory          |   Mandatory        |  
|   **Understand Care Context**                     |   Mandatory           |   Mandatory        |  
|  **Link Care Context**                    |        |           |  
|   HIP Initiated Linking             |   Mandatory           |   Mandatory | 
|   Notification to Mobile             |   Mandatory           |   Mandatory | 
|   Discovery & Linking            |   Mandatory           |   Mandatory | 
|   **Understanding Consents**             |   Mandatory           |   Mandatory | 
|  **Store Consent Artefacts**  |  Mandatory                    |  Mandatory                 |                
|   **Request Health Records**     |   Mandatory          |   Mandatory        |  
|   **Packaging Health Data**         |   Mandatory          |   Mandatory        |  
|   **Encryption & Decryption**             |   Mandatory          |   Mandatory        |  
|   **Transferring Health Data**  |   Mandatory          |   Mandatory        |   


## This section covers:
{{% notice %}}
1. Health Record formats
2. Understanding care context
3. Linking care context
	- HIP initiated linking 
	- Notification to mobile
	- Discovery & Link
4. Understanding Consents
5. Storing consent notifications
6. Request for Health Records  
7. Packaging Health Data
8. Transferring Health Data
{{% /notice %}}
