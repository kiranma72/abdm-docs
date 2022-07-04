---
title: "UHI Architecture Overview"
date: 2022-05-07T18:00:04+05:30
Weight: 2
draft: false
---
### UHI Architecture 

UHI aims to transform the way digital health services are rendered in India, while ensuring that it is in sync with the other building blocks of ABDM. The functional architecture for UHI is mentioned below. The aim of this architecture is to ensure interoperability for health services and health data. The architecture also depicts how UHI will interact with the other building blocks within ABDM. 

![UHI Architecture Overview](https://github.com/kiranma72/abdm-docs/blob/2918a64c07143dc71519699d3caf569086448dff/content/UHI/UHI_%20Architecture_Overview.png)

#### Architecture Steps 

**1.A Patient Sign Up/ Login:** Patients login using their ABHA number/ Aadhar number / Mobile Number. This is verified by HIE-CM (for login via ABHA number) and UIDAI (for login via Aadhar) through an OTP authentication, post which the login is enabled. In case patients do not have an account, they are asked to sign up using their Aadhar or by providing any other identification documents. 
   
**1.B Health Service Provider Sign Up/ Login:** Health Service Providers (HSPs) login using their HPID/ HPR Address (Health Professional Address) on thw HSPA. In case the HSP does not have a Health Professional Address, he/she will be asked to create one using their Registration Number registered with their respective State Council. 

**1.C Health Service Provider Details sent to HPR:** The details filled by the the Health Service Provider are sent back to the Health Professional Registry. 

**2. Patient Search for a Doctor:** A patient searches for a doctor on the EUA via defined parameters. The EUA fires Search API to the  UHI Gateway to look for the doctors matching the search criteria across the network.

**3. Search Request Sent to all Registered HSPAs:** The UHI Gateway broadcasts the search request and the search parameters to all the HSPAs registered on UHI. 

**4.A Matching HSPAs Respond:** All HSPAs that match the criteria sent by the gateway respond to the request via on_search. HSPAs send back x, y and z. The gateway forwards all responses back to the EUA. 

**4.B HSPAs Directly Send Availability to EUAs:** While x, y and z is sent via the gateway, as mentioned in the step above, the HSPAs send the availability of a chosen HSP directly to the EUA. This is done via on_search API. 

**5. Patient Initiates Booking:** The patient choosen any available slot and initiates booking on the EUA. The EUA calls innit API through which it sends the order details.

**6. HSPA Responds to Booking:** The HSPA responds via on_innit API and also sends the payment terms for the transaction.


