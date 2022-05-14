---
title: "Making your App ABDM Compilant"
date: 2022-05-07T18:00:04+05:30
Weight: 5
draft: false
---

The healthcare ecosystem has various types of applications. These include

1. HMIS / LMIS systems -- Anyone providing a healthcare software to hospitals, labs, clinics, etc 
2. Consumer Healthcare applications -- Personal Health record applications, Teleconsultation applications, etc. Anyone building healthcare applications for consumers / patients  
3. Government Health apps  -- Software providers for goverment programs like RCH, NCD, NIKSHAY, COWIN, etc

Each of the above apps can play multiple roles in the ABDM ecosystem depending on their requirement. 

First decide on the roles that your application will play in the ABDM ecosystem 

 | Role | Applicable to | Example Applications | 
 | -----| ----------- | ------------------- |
 | HRP / HIP | Any application that holds health records and shares it on demand | HIMS, LIMS, Teleconsultation Apps, user uploaded data in PHR apps, Government programs, etc | 
 | HIU | Any application that requires access to user health records | HIMS, Teleconsultation Apps, PHR apps, Insurance apps | 
 | PHR App | Consumer applications that want to help users manage their health records & consents | PHR Apps | 
 | Integrated Programs | Healthcare applications from the goverment | CoWIN, Nikshay, eHospital, PMJAY, |  

ABDM compliance testing will be have to be passed for each role you wish to support in your application 

For an explaination of the various roles read the [PHR Architecture Overview](/abdm-docs/1-basics/phr_architecture_overview/)

## Features to be supported by a HRP / HIP

1. Register health facilities (HIPs) and link it to your software (HRP) endpoint
2. Collect & Verify ABHA address during patient registration (Milestone 1) 
3. Help users discover their health records available in your system (Milestone 2)
4. Notify or link a new health record with a ABHA address when it is created in your system (Milestone 2) 
5. Share the health record on request after verifying user consent (Milestone 2) 
6. Structure the health record in an inter-operable format using FHIR (Milestone 2)
7. Support Consent revokes, deletion of ABHA address and uptime related heartbeats (Milestone 2) 

## Features to be supported by a HIU

1. Request access to health records linked with a ABHA address (Milestone 3) 
2. Fetch linked records from HRPs (Milestone 3)
3. Organize and display fetched health records (Milestone 3) 


## Features to be supported by a PHR app

1. Issue a ABHA address to the user 
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

1. Issue an unique ABHA No to the user
2. Create a linked ABHA address 
3. Link health records to ABHA No
4. Fetch health records from ABHA No





