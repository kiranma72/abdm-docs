---
title: "Bahmni"
date: 2022-05-15T18:00:04+05:30
Weight: 6
draft: false
pre : "<b>1.6 </b>"
---


## Bahmni

Bahmni is an OpenMRS Distro. It is an open source EMR and a full Hospital Management System with Lab, Billing, Pharmacy, PACS and other integrated features. An instance of Bahmni has been setup to act as a Health Information Provider and Health Information User in the ABDM Sandbox. This can be very useful for testing the following use cases during ABDM integration. 

- To see examples of how Milestone 1 is integrated in a HMIS / LMIS
- To test Milestone 3 if you are integrating the same in a HMIS or PHR app
- To test most of the PHR app related testcases that require a HIP / HIU

## Who is developing Bahmni?

Thoughtworks started building Bahmni in January 2013 as part of its mission of social and economic justice. In October of 2017 Thoughtworks transferred ownership of Bahmni to the Bahmni Coalition under the Fiscal Sponsorship of the non-profit OpenMRS, Inc. Thoughtworks continues to be a major contributor to Bahmni, and serves on its Governing Committee.
Bahmni is built by the Bahmni Coalition, and other open-source contributors.The Coalition is a group of companies and non-profit organizations who work together under the Fiscal Sponsorship of the non-profit OpenMRS Inc, to develop, implement, and use Bahmni.

## How is Bahmni ABDM integrated?

Bahmni is ABDM compliant, i.e it has successfully integrated all the required milestones/ guidelines mandated by the NHA to be an ABDM compliant software. Bahmni can be deployed as an ABDM compliant Hospital Management System which facilities can adopt to integrate seamlessly with the ABDM ecosystem 

With Bahmni, 

- The user can capture and verify the ABHA ID  and fetch the demographic information of the patient.

- The facility can act as a HIP, i.e. create medical records which can be shared digitally.

- The facility can act as a HIU, i.e. request and  view patient’s records with consent.

## Bahmni Environment

The LITE version of Bahmni, (ABDM Compliant) configured for clinics and small hospitals. It comes with the CIEL dictionary, and ABDM components. To access the hosted instance that is linked with the ABDM sandbox use

URL: https://dev.lite.mybahmni.in/

The environment is currently available only during India hours (8am-9pm IST daily).
If you need it up longer for specific demos, please contact bahmni via SLACK. 

Please ping on Slack #bahmni-infra channel if you are have issues while accessing the link.

Note : HIU/HIP id for the above Bahmni environment


```json
{
        "identifier": {
            "name": "Bahmni",
            "id": "Bahmni"
        },
        "telephone": null,
        "city": null,
        "latitude": null,
        "longitude": null,
        "address": null,
        "districtCode": null,
        "stateCode": null,
        "pinCode": null,
        "facilityType": [
            "HIP",
            "HIU"
        ],
        "isHIP": true,
        "attributes": {
            "hipAttributes": null,
            "hiuAttributes": null,
            "healthLockerAttributes": null
        }
    }
```


**Credentials**

 - Bahmni EMR:

    *Usernames:* superman, dr_neha, registration

    *Password:* Admin123

 - HIU:

    *Username:* admin

    *Password:* nimda

Please be aware that multiple integrators will use the same login / credentials. This support from Bahmni is being provided to support the ABDM community. Share the love & care. 

## Landing Page & Login Page 

{{< gallery dir="1-basics/Bahmni_page" />}} {{< load-photoswipe >}}

## Communication Tools

- **Discussion Forum:**

    The primary place to communicate about Bahmni is the Discussion Forum. The Bahmni forums are hosted under the "OpenMRS Talk" discussion forums" (a section of OpenMRS's discussion forum)

- **Chat on Slack:**


  *Signing up on Bahmni Slack*
   - For quick chat-style messages, active Bahmni contributors use Slack.
   - Most communications are on the #community channel. There are other channels for project (or topic) specific discussions.

  *Slack info*

    - URL: https://bahmni.slack.com

    - Login:

        - If you belong to an organization whose domain name has already been pre-approved, then you may create your own account.
        - Otherwise the users can also make the request on the discussion forums, via https://www.bahmni.org/contact-us/



