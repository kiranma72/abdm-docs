---
title: "Making your App ABDM Compliant"
date: 2022-05-07T18:00:04+05:30
Weight: 8
draft: false
pre : "<b>1.8 </b>"
---

To become an **ABDM Compliant Application**, your application needs to implement specific functional capabilities and pass functional validation.  

The functionality has been broken into milestones to make it easier to implement. Your first step is to understand the functionalities that your application must support. This depends on what type of application you are integrating. 


Certification Functionality to be implemented|M1|M2|M3|Locker |Integrated Programs|HFR|HPR
 | ------------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
HMIS Applications - Used by Hospitals |Yes|Yes|Yes|NA|NA|Yes|NA
LMIS Application - Used by Labs|Yes|Yes|NA|NA|NA|Yes|NA
PHR Application - For consumers|Yes|Yes|Yes|Yes|NA|NA|NA
Public Health Application - Used by Health Workers|Yes|Yes|Yes|No|Yes|Yes|NA
Teleconsultation Application |Yes|Yes|Yes|No|No|Yes|Yes|

Each functionality is defined by detailed test cases that must be passed to to obtain ABDM compliance.

Here is a quick list of functionalities that must be implemented for each milestone certification:
## Features to be supported for Milestone 1 (M1)
1. Create ABHA number & address - using Aadhaar / Mobile / Driving License
2. Collect & Verify ABHA address during patient registration

## Features to be supported for Milestone 2 (M2)
**Description:** This milestone enables a health care entity/professional to become Health Information Provider (HIP). This implies that the clinical artifacts generated will be linked with the ABHA and is ready for consent-based-sharing within ABDM eco-system. Patient will be able to view the generated and linked health records in any of his/her preferred PHR app downloaded in the mobile device. Functionalities offered are:
1. Help users discover their health records available in your system 
2. Notify or link a new health record with a ABHA address when it is created in your system
3. Share the health record on request after verifying user consent
4. Structure the health record in an inter-operable format using FHIR
5. Support Consent revokes, deletion of ABHA address and uptime related heartbeats 

## Features to be supported for Milestone 3 (M3)
**Description:** Completion of this milestone enables a healthcare entity/professional to become Health Information User (HIU). This milestone enables exchange of health data between healthcare entities or healthcare professionals or with a health locker based on patient authentication only. Any entity seeking health records for treatment/diagnosis is termed as Health Information User (HIU). Functionalities offered are:
1. Request access to health records linked with a ABHA address
2. Fetch linked records from HRPs 
3. Organize and display fetched health records 


## Features to be supported by a PHR app

1. Issue ABHA address to the user 
2. Link the ABHA address to a ABHA No if requested by the user 
3. Login (authenticate) the user 
4. Share user profile during registration at a healthcare provider
5. Discover user records at a healthcare provider
6. Link health records discovered by the user to their ABHA address
7. Notify users when any new health records are linked to their ABHA address
8. Raise consent requests and fetch newly linked records (Milestone 3)
9. Organize and display fetched health records
10. Help the user manage their consents & subscriptions 
11. Scan / Upload records held by the user and link it to their PHR address
14. Act as a HRP for users health records and share it on demand 
15. Help users edit their profile, delete ABHA address 

## Features to be supported by Integrated programs

Goverment Health programs need to mandatorily support the following additional features apart from any of the above roles

1. Issue an unique ABHA No to the user using offline methods
2. Create a linked ABHA address 
3. Link health records to ABHA No
4. Fetch health records from ABHA No


