---
title: "Making your app ABDM compliant"
date: 2022-05-07T18:00:04+05:30
Weight: 4 
draft: false
---


 First decide on the roles that your application will play in the ABDM ecosystem 

 | Role | Applicable to | Example Applications | 
 | -----| ----------- | ------------------- |
 | HRP / HIP | Any application that holds health records and shares it on demand | HIMS, LIMS, Teleconsultation Apps, user uploaded data in PHR apps, Government programs, etc | 
 | HIU | Any application that requires access to user health records | HIMS, Teleconsultation Apps, PHR apps, Insurance apps | 
 | PHR App | Consumer applications that want to help users manage their health records & consents | PHR Apps | 


For an explaination of the various roles read the [PHR Architecture Overview](/abdm-docs/1-basics/phr_architecture_overview/)

## Features to be supported by a HRP / HIP
Entities providing a healthcare software to hospitals, labs, clinics, etc comes under this category.

HIMS Maintain, collect and manage health records. Ensure timely and accurate delivery of data to health care providers. 
In return the health care providers rely on the information to deliver quality healthcare

LIMS is a software designed to improve lab productivity an---
title: "Verify you can access the Sandbox"
date: 2022-05-07T18:00:04+05:30
Weight: 4 
draft: false
---
d efficiency, by keeping track of data associated with samples, experiments, laboratory workflows, and instruments

The private HIMS partners are Piramal Swasthya, Narayana Health Limited, Drucare Private Limited, Apollo hospital,  Plus 91, Thoughtworks, DocOn Technologies and Bajaj Finserv Health

The private LIMS partners are SRL LIMITED,  Livehealth and Dr Lal PathLabs.

**Benefits:**
- Ease of sharing patient's health records to other hospitals with their consent
- Reduces redundancy of Pateint's Data 
- 

**Features:**

What are the key functionalities that must be supported by your system to become ABDM compliant

1. Register the health facility that uses your software and link it to your software endpoint
2. Creation of ABHA (Health IDs)
3. Verification of ABHA (Health IDs)
4. Profile Sharing using QR Code
5. Linking of Patient specific health record against a specific ABHA id
6. Help users discover their health records available in your system
7. Notify or link a new health record with a ABHA address when it is created in your system
8. Share the health record on request after verifying user consent
9. Support revokes, deletion of ABHA addressess and heartbeats that verify uptime
10. Request access to health records linked with a ABHA address
11. Obtain and organize health records for a ABHA address (Milestone 3)
12. How do you format your health records to be inter-operable using FHIR
13. New capabilities coming soon to ABDM -- UHI & HCX








## Consumer Healthcare applications

Entities building health care applications for consumers / patients comes under this category.

The private Healthcare application partners are Curelink Private Limited, Alafied Solutions Private Limited, Practo, Verraton Health Private Limited, MarSha Health, 
NEC Software Solution, Jio Health Hub, Raxa Health, Doxper, argusoft MEDplat and Pristyn Care

The healthcare applications 

**Benefits:**
- Faster registration process 
- Reduces data entry errors
- Way to share/get medical history
- Sharing health information with patient and other user in a national standard
- Get medical history of patient with their consent

**Other Benefits:**
1. UHI 
2. Users can book appointment
3. Tele consulting
4. Users can Book ambulance
5. Provides all list of hospitals
6. Health Claim Exchange(HCX) - can raise the insurance claim with government and private insurance processing

**Features:**

What are the key functionalities that must be supported by your system to become ABDM compliant

1. Issue a ABHA address to the user
2. Link the ABHA address to a ABHA No if requested by the user
3. Login (authenticate) the user
4. Share user profile during registration at a healthcare provider
5. Discover user records at a healthcare provider
6. Link health records discovered by the user to their ABHA address
7. Notify users when any new health records are linked to their ABHA address
8. Automatically fetch new records that are linked to the ABHA address
9. Raise a consent request to fetch linked health records
10. Obtain a copy of the linked health record
11. Display users health records
12. Help the user manage their consents & subscriptions
13. Scan / Upload records held by the user
14. Share the health record on request after verifying user consent (Milestone 2)


## Government Systems

Entities providing software for the government programs like RCH, NCD, NIKSHAY, COWIN, etc should start here




