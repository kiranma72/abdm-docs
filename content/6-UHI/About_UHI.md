---
title: "UHI Protocol"
date: 2022-05-07T18:00:04+05:30
Weight: 1
draft: false
---

### What is UHI?

The Unified Health Interface (UHI) is a network where applications built on the UHI open protocol can interoperably connect with each other to provide health services. UHI is a key Digital Public Infrastructure that enables discoverability and transaction for digital health services.  UHI works with other ABDM building blocks like HIE-CM for interoperable exchange of personal health data and  registries like HPR & HFR to enable trust from participating doctors and health facilities. UHI takes an ‘Open Network’ approach to build the gateway and to enable the creation of a nationwide, decentralized, open, and inclusive network. 

ABDM manages the UHI Gateway and the UHI Registry. Any application that wishes to participate in UHI must 

- Implement the UHI protocol  
- Register with the UHI registry 
- Use the UHI Gateway to discover other UHI apps & their services
- Comply with the UHI Market Rules 
- Share metrics with UHI for reporting, greviance redressal and dispute resolution 

It will be provide a system to facilitate the discovery of services between user facing applications and health service provider applications. Open access across diverse health service providers and patients can drastically expand demand-supply ecosystems and transform the digital healthcare landscape in India.

### What is UHI Open Protocol? 
UHI Open Protocol is a Decentralized Health Protocols aimed to define the interoperable protocol specifications for creating a decentralized network of health services. The purpose of APIs is to enable interoperability between Healthcare providers (doctors, paramedical, health facilities, etc.) and Healthcare consumers. The UHI Open Protocol architecture and APIs allow individuals/ organizations to set up an open network of consumer side applications and health service provider side platforms using common protocol specifications. It renders open APIs, schemas and example flows for the different use cases in healthcare. 

The protocol is being developed as an open community initiative on GitHub [https://github.com/dhp-project/DHP-Specs](https://github.com/dhp-project/DHP-Specs)


### UHI Services 

The services on UHI will include, but not be limited to

- Teleconsultation 
- Booking Physical Appointments 
- Lab Bookings 
- Ambulance Services  
- Blood Donation 

### UHI Participants 

Any service transaction in UHI involves five entities:

**User**: Patients seeking digital health services through UHI. 

**End User Application (EUA)**: User-facing applications offering digital health services 

**UHI Gateway**: Layer routing the initial requests and responses involved in UHI transactions between HSPAs and EUAs

**Health Service Provider Application (HSPA)**: Provider-facing applications allowing doctors to respond to EUA requests and fulfill digital health services 

**Health Service Provider (HSP)**: Providers of healthcare services

### Role of the UHI Gateway 

The role of the gateway in a UHI service transaction is limited to the search and discoverability of health services. For example, if a user searches for teleconsultation services on an EUA, the gateway routes the request to all available HSPAs and sends back the responses to the EUA. The booking, payment and fulfillment of the service, thereafter, is done directly between the EUA and the HSPA. 

![UHI Gateway Overview](https://github.com/kiranma72/abdm-docs/blob/a6ffaccda810a85dc880457ea446574ed271bd2e/content/UHI/UHI_Gateway_Overview.png)





