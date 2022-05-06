# Overview of FHR framework

Using the Federated Health Records framework (FHR), patients can access and view their health records, and provide consent to any HIPs and HIUs to access their data. 
This works in two ways:

- Any HIU can request a patient’s information from an HIP, and obtain it through patient’s consent.

- Any HIP can directly request the patient for consent to access their information.

Patients can also selectively share their data with any HIU or HIP through the patient’s mobile interface in the FHR Framework. FHR Framework removes the limitations 
faced by patients and medical practitioners, enabling all parties involved to make informed decisions and ensure better, and more seamless, quality of care.


## What is an HIP?
An HIP (Health Information Provider) can be a hospital, laboratory, health care center, clinic or pharmacy - basically any entity which creates medical data 
pertaining to a patient. By agreeing to be part of this federated health records system, health care providers take on the role of Health Information Providers 
(HIPs), who are willing to share the data through the system. HIPs are required to maintain a digital copy of both the inpatient and outpatient records for each 
person in their care. In order to become an HIP, the said health care facility will need to enrol in the ABDM health care infrastructure registry.


## What is an HIU?
An HIU (Health Information User) is an entity that wants access to digital health information from HIPs, in order to provide services to the patient to 
whom the information belongs. An HIU can be a hospital, clinic, healthcare technology company, organizations working on health analytics, insurers, medical 
researchers and government entities. These HIUs will be able to request for health records of a patient, and upon obtaining the patient’s digital consent, view 
the health records for a limited time period.


## What is a Personal Locker?
The Federated Health Records exchange system stores patients’ information as longitudinal records, i.e, electronically searchable, with flagged abnormal values 
provided directly within the patient’s health chart. HIUs are required to manage a software system that enables them to securely store and access the longitudinal 
patient information in their care. A patient’s longitudinal health records are stored in a trusted location, either on the patient’s personal devices or on a 
user-trusted cloud service. Such a software system is referred to as a personal health locker.


## The FHR Sandbox Environment
ABDM is providing a sandbox environment with core essential services that enable HIPs and HIUs to rapidly test their integration. 
Implementers will use the sandbox platform environment with representative Gateway, Consent Manager and Registries to enable HIP and HUI services. 
The FHR sandbox environment will be used particularly to share only patients’ personal information with HIPs and HIUs.

We aim bring the following goals to fruition via the FHR framework:

- Deliver better quality of care by establishing an ecosystem of connected healthcare systems.
- Enable HIUs such as hospitals and labs to access patient care information,while ensuring patients' privacy and confidentiality.
- Leverage tiered approach of care delivery.

# ABDM digital health architecture
## Overview of architecture
The FHR architecture is inline with the concepts described in the Niti Aayog National Health Stack (NHS) strategy and approach concept paper1 published in July 2018.

As stated in the National Health Digital Mission (ABDM) operational strategy, the architecture is modelled as a Federated Architecture, where management and data access occurs in a 'federated' manner — where multiple entities will manage health data about users. The federated architecture will enable current and future health information flowing through the system, for example between providers and patients, wearables and EHR/EMRs, consumers and physicians, labs, institutions and payers. A centralized approach, where collation of data in National Repositories for democracy like ours with a 1.35 billion population will be prohibitively expensive and increase friction with the ecosystem, would be a single point of failure, with any security breach resulting in unimaginable compromise. A federated system allows data to sit at the source and be accessible on demand.

Healthcare service provides need patient's health information in order for them to provide effective care. Insurance providers need hospitalisation and diagnostic data for processing claims. In such scenarios, it is essential that users and patients provide consent to providers sharing data, to safeguard patients' privacy and data.

To ensure smooth consented data sharing and time-bound data access, it is necessary to make the data traceable and auditable. Therefore the FHR Framework architecture leverages MeitY's Data Empowerment and Protection Architecture (DEPA)2 electronic consent framework, which is already being used in financial sectors, notably in NBFC Account Aggregator3 framework.

The following diagram represents the overall digital health architecture that corroborates with the ABDM vision for digital health in India:

 ![ABDM digital health architecture](/resources/ABDM_digital_health_architecture.png)
 
 
The digital health architecture is composed of the following:

- A set of core services, inclusive of National Level Electronic Registries such as Doctor Registry and Facility Registry
- FHR framework components such as gateway, consent manager and health repositories

## Other relevant documents
1. National Digital Health Blueprint
2. National Health Stack
3. Electronic Consent Framework

# FHR framework components & roles
The following section describes the roles played by the various entities represented in the FHR architecture.


## Health data consent manager (HDCM)
HDCM plays the role of fiduciary or trustee with which a patient signs up to begin with. The HDCM does the following:

- Helps to create or discover existing ABDM ABHA Number
- Manages patient linkages to providers
- Manages consent for access to health information
- Helps discover patient information
- Monitors information exchange between HIP and HIU
All the above are done via a Patient App. In future, there will be other channels for patients to manage their health data.

## Health information gateway
Gateway is the hub that mediates and connects Consent Manager(s), Health Repository Providers and HIUs in the network. 
Its primary job is to allow for discovery, routing in the network. The gateway does the following:

- Connects and validates the HDCMs and health repositories (servicing HIUs and HIPs) to the network.
- Enables routing of information.
- Authenticates connected systems within the FHR Framework (provides a signed authentication token for further communication). 
The entire FHR framework including the gateway communicates via asynchronous APIs over HTTPs channel.

## Registries
There are various National level Registries that are integrated with the network.

- Health Facility registry (HFR)
- Doctor or practitioner registry (DigiDoctor)
- HDCM and Health Repository Provider (HPR) Registry

The HDCM and HRP registries are currently maintained by the ABDM Gateway.

## Health repository
A health repository is the connector or bridge through which any HIU or HIP can connect to the network. 
The health repository allows HIPs and HIUs to access patient data for a specific period of time. 
The sandbox environment provides a basic HIU system, representing a doctor's interface. 
The sandbox environment also provides a mock HIP system using which you can test linkages and access to health information from multiple sources.


## HIP services
The following responsibilities are expected to be carried out by HIP services in the FHR Framework context:

- Ability to discover and link patient's care contexts within an organization's system.
- Allow for consented means of exchange of patient's health information in a machine readable format (FHIR), conforming to standards setup by ABDM.
- Provide a secure and safe means of data transfer from organization-specific HIS (Health Information System) instance to a validated 
and consented requester HIU, through the ABDM Gateway.


## HIU services
The following capabilities are expected of HIU services in the FHR context:

- Ability to search for and identify a patient using her ABHA Number. HIU systems can search for patients linked within the ABDM Gateway network, 
and across diverse Gateway networks in future.
- Ability to request and receive patient data in a safe and secure manner, manage data lifecycle, and enable secure data storage and access.

## Health locker services
Health locker provides a personal digital storage for users/patients. The following capabilities are expected of Health locker services in the FHR context:

- Sign up users/patients in their system.
- Allow users to upload their health documents to their locker.
- Ability to fetch users health documents from the HIPs based on patient consent.
- Ability to Provide Health Documents, both self uploaded and fetched from HIPs, to a valid requester (HIU) based on patient consent.
- Allow user/patient access to their health documents (through their locker apps or other channels).
- Provide secure means for health document access and storage.

## What is a Patient App?
While building and testing your health repository in integration with the sandbox's network components, you'll need to test patient flows as well. For example:

- Signup of patient with Consent Manager (CM)
- Linking patient's CM account with HIP's patient reference and health care contexts
- Granting or revoking consents

You can do all of the above using APIs as well, but the easiest way would be to use the reference patient Android App. Download .apk file.
