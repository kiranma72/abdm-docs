+++
title = "UHI"
date = 2023-05-11T07:53:25+05:30
weight = 8
chapter = true
pre = "<b>8. </b>"
+++

# UHI & UHI Network

UHI is **envisioned as an open protocol for various digital health services.** UHI Network will be an open network of End User Applications (EUAs) and participating Health Service Provider (HSP) applications. 

- UHI will **enable a wide variety of digital health services** between patients and health service providers (HSPs) including, but not limited to:

	- Booking OPD appointments at hospitals / clinics
	- Booking Tele-Consultation
	- Discovering availability of critical care beds
	- Discovery of lab and diagnostic services
	- Booking of home visits for lab sample collections
	- Booking an ambulance
	- Discovery of nearby pharmacies

**End user application (EUA)** is any application chosen by the service consumer (frequently referred to as user) to access Health services. EUAs can be of diverse forms like mobile apps, interactive voice response systems (IVRS), virtual assistants in English and local languages, etc. 

Health service providers may be individual doctors, hospitals, labs, pharmacies, companies that aggregate health services, etc. They provide digital health services using Health Service Provider Applications (HSPA) that support UHI. 

**UHI ensures that a digital health service can be delivered between any EUA with any HSP in this ecosystem.**

**UHI Services**

The services on UHI will include, but not be limited to

- Teleconsultation
- Booking Physical Appointments
- Lab Bookings
- Ambulance Services
- Blood Donation

**UHI Participants**

Any service transaction in UHI involves five entities:

- **User:** Patients seeking digital health services through UHI.

- **End User Application (EUA):** User-facing applications offering digital health services

- **UHI Gateway:** Routing the initial service/provider discovery requests and responses involved in UHI transactions between HSPAs and EUAs

- **Health Service Provider Application (HSPA):** Provider-facing applications allowing health service providers (doctors, health facilities etc) to respond to EUA requests and fulfill digital health services

- **Health Service Provider (HSP):** Providers of healthcare services

### Role of the UHI Gateway

The role of the gateway in a UHI service transaction is limited to the search and discoverability of health services. For example, if a user searches for teleconsultation services on an EUA, the gateway routes the request to all available HSPAs and sends back the responses to the EUA. The booking, payment and fulfillment of the service, thereafter, is done directly between the EUA and the HSPA.

![uhi gateway](/abdm-docs/img/uhi-gateway.png)  

Check out the [**UHI Starter Guide**](../Unified_Health_Interface_Starter_Guide.pdf)

Check out the [**Catalog Mandatory Requirements document for UHI**](https://docs.google.com/spreadsheets/d/14HSsyn1tNaxmXO4y21a4OiXaEID5FbeVLWJXX52OX3E/edit?usp=sharing)

Here is the link to [**Sandbox Request Form**](https://sandbox.abdm.gov.in/applications/Home/signup_form_UHI)