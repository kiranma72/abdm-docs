---
title: "About ABDM Sandbox"
date: 2023-03-07T18:00:04+05:30
Weight: 2
draft: false
pre : "<b>1.2 </b>"
---


The **Ayushman Bharat Digital Mission** (ABDM) has developed building blocks and APIs to offer a seamless digital healthcare experience for all stakeholders – health facilities, patients and healthcare workers. The digital infrastructure developed is now accessible to health facilities and health tech players for integration.

Here's a picture to help you understand how ABDM can improve the experience you deliver to your patients :

![Experience](../experience.png)

## ABDM Sandbox Journey

ABDM aims at bringing out inoperability and sharing of health information among all the participants in India. For this to happen, we expect organizations that build software for hospitals, labs, insurers, consumers to implement certain functionalities by integrating with ABDM building blocks. The ABDM sandbox provides tools and support to test the integration. Once integrated, the software developers (companies) can get independent functional validation and apply for ABDM certification (by applying for Sandbox Exit). The certified version of the software can then be deployed for the various health service providers.

Here's how your **journey through the sandbox looks like:**

![Integration journey](../sandbox-integration-journey.jpeg)


1. Register for access to the Sandbox 
2. Receive a Sandbox client ID & secret (key) from National Health Authority (NHA)
3. Understand the various functionalities (test cases) to be implemented for each integration milestone
4. Get comfortable with the APIs for each functionality using Postman
5. Implement the functionality in your application
6. Get functional validation report from one of the 3 empanelled companies
7. Get security test report from any CERT-in empanelled organization
8. Apply for Sandbox Exit
9. Demo your app to NHA team
10. Obtain a Production client ID & secret (key) from NHA
11. Deploy your ABDM certified application with your customers


## ABDM Integration Milestones
The integration steps have been broken into milestones to make it easier for integrators. Each Milestone has a set of functional test cases that must be supported by your application as part of certification
- **Milestone 1**: ABHA Number creation and capture & verification for seamless patient registration.[{{% icon icon="download" %}}](https://sandbox.abdm.gov.in/documents/ABHA_APIs.xlsx)
- **Milestone 2**: Building Health Information Provider (HIP) services to share digital records via any Personal Health Records (PHR) app. [{{% icon icon="download" %}}](https://sandbox.abdm.gov.in/documents/Milestone_M2_APIs.xlsx)
- **Milestone 3**: Developing Health Information User (HIU) services to provide view of patient’s medical history to authorized healthcare workers with complete consent
- **PHR & Locker Apps**: Subscriptions for notifications, helping users manage consents, upload of user scanned records and more 



## Before you start integration

- Check which milestones are applicable for your [type of application here](/abdm-docs/1-basics/making_your_app_abdm_compliant/)
- Understand the concepts & functionality required for each milestone
- Review the test cases for each milestone
- Download the Postman collection and validate each API that is part of a test case in the sandbox
- Integrate the APIs with your application once you are confident on how it works using Postman 

