ABDM allows various types of entities to integrate with their APIs. Please choose the approprate type that fits your application from the choices below.

1. HMIS / LMIS systems -- Anyone providing a healthcare software to hospitals, labs, clinics, etc should start here 
2. Consumer Healthcare applications -- Personal Health record applications, Teleconsultations, etc. Anyone building healthcare applications for consumers / patients should start here 
3. Government Systems -- Any software provider for goverment programs like RCH, NCD, NIKSHAY, COWIN, etc should start here

## HMIS / LMIS Systems

Please read the ABDM concepts overview first 

What are the key functionalities that must be supported by your system to become ABDM compliant 
0. Register the health facility that uses your software and link it to your software endpoint
1. Collect & Verify ABHA address during patient registration (Milestone 1) 
2. Help users discover their health records available in your system (Milestone 2)
3. Notify or link a new health record with a ABHA address when it is created in your system (Milestone 2) 
4. Share the health record on request after verifying user consent (Milestone 2) 
5. Support revokes, deletion of ABHA addressess and heartbeats that verify uptime (Milestone 2) 
6. Request access to health records linked with a ABHA address (Milestone 3) 
7. Obtain and organize health records for a ABHA address (Milestone 3) 
8. How do you format your health records to be inter-operable using FHIR 
9. New capabilities coming soon to ABDM -- UHI & HCX 


## Consumer Healthcare applications
Please read the ABDM concepts overview first 

What are the key functionalities that must be supported by your application to become ABDM compliant 
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



