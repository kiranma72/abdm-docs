---
title: "About ABDM Sandbox"
date: 2023-03-07T18:00:04+05:30
Weight: 1
draft: false
pre : "<b>1.1 </b>"
---

## ABDM Sandbox

The **Ayushman Bharat Digital Mission** has developed building blocks and APIs to offer a seamless digital healthcare experience for all stakeholders – health facilities, patients and healthcare workers. The digital infrastructure developed is now accessible to health facilities and health tech players for integration.

Here's a picture to help you understand different interaction touchpoints of a patient with the system:

![Experience](../experience.png)

## ABDM Sandbox Journey

ABDM aims at bringing out inoperability and sharing of health information among all the participants in India. For this to happen, we expect the software developers to implement certain functionalities by integrating with ABDM building blocks.
Integration with ABDM sandbox is designed for them to test the integration. Once integrated, the software developers (companies) can get independent functional validation and apply for ABDM certification (called as Sandbox Exit) via Sandbox.
The certified version of the software can then be deployed for the various health service providers.

Here's how your **journey through the sandbox looks like:**

1. Submit your Sandbox application
2. Receive a Sandbox client ID & secret (key) from National Health Authority (NHA)
3. Understand the various functionalities (test cases) to be implemented for each milestone
4. Ensure you are comfortable with the APIs to implement each functionality (using Postman)
5. Implement the functionality in your application
6. Get functional validation report from one of the 3 empanelled companies
7. Get security test report from one of the 3 empanelled companies
8. Apply for Sandbox Exit
9. Demo your app to NHA team
10. Obtain a Production client ID & secret (key) from NHA
11. Deploy your certified application with NHA

## Building Blocks
The Sandbox hosts of the following digital building blocks that are useful for anyone wanting to comply to the HIP, HRP and HIU guidelines:

1. ABHA Number Service - Create a ABHA Number, integrate your software with the ABHA Number APIs
2. Consent Manager and Gateway - Register your software as a HIP or HIU and ensure you are able to correctly link records, process consent requests
3. Sandbox ABHA Mobile Application for Android - Use the application to manage your ABHA Number, view health records and manage consents
4. Sandbox HIU application to create consent requests for a ABHA Number
5. Sandbox DigiDoctor and APIs to register and verify doctors
6. Sandbox Health Facility Registry and APIs to register and verify facilities

## ABHA Sandbox Setup Milestones
It is recommended developing this experience in three milestones, each building over the previous:
- **Milestone 1**: ABHA Number creation and capture & verification for seamless patient registration.[{{% icon icon="download" %}}](https://sandbox.abdm.gov.in/documents/ABHA_APIs.xlsx)
- **Milestone 2**: Building Health Information Provider (HIP) services to share digital records via Personal Health Records (ABHA) app. [{{% icon icon="download" %}}](https://sandbox.abdm.gov.in/documents/Milestone_M2_APIs.xlsx)
- **Milestone 3**: Developing Health Information User (HIU) services to provide view of patient’s medical history to authorized healthcare workers with complete consent

## ABHA Address

Hospitals & Labs are expected to link records with their patients ABHA Address (also called PHR address)
Creating an PHR (Public Health Record) Address is super simple – all it needs is your Name, Year of birth, Gender along with a Mobile number.

Key benefits of creating an PHR Address are:
- Easy access to health information in a paperless manner
- Voluntary opt-in and opt-out at anytime
- Enables authentication for consent driven access to health data along with capabilities  to manage and revoke consent
- Inclusive access to people with smartphones, feature phones, and even no phones using assisted methods
![Get ABHA Address](../Abha-address.png)

This section offers step-by-step guidance on the following for interested stakeholders:
Guidelines to integrate ABDM-powered services (ABHA Number capture & verification, HIP services, HIU application) in the testing environment called Sandbox
More details are provided in the given document
Process to exit sandbox and deploy application in facilities located across all States and UTs.
