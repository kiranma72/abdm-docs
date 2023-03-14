---
title: "The PHR Framework"
date: 2022-05-07T18:00:04+05:30
Weight: 2
draft: false
pre : "<b>1.2 </b>"
---

ABDM uses a federated architecture to help users collect their health records across various healthcare providers, view their records from any PHR application and share their records with any requestor with their consent 

The image below shows the various entities/roles involved in the PHR framework

![ABDM HIP HIU Architecture](../phr-architeture.pptx.jpg)

## What is a Health Information Provider (HIP)?
Any entity that agrees to share digital health records with their users using the [ABDM specified methods](https://old.abdm.gov.in/assets/uploads/HIP_HIU_Policy.pdf) is called an HIP (Health Information Provider). HIPs can be hospitals, labs, health care centers, government health programs, teleconsultation players, clinics or pharmacies - basically any entity which creates medical data pertaining to a patient. 

HIPs are required to maintain a digital copy of both the inpatient and outpatient records for each person in their care. In order to become an HIP, health facilities must enrol in the ABDM [health facility registry](https://facility.abdm.gov.in)

## What is a Health Repository Provider (HRP)?
 Health repository providers are software service providers who offer ABDM compliant software to health facilities like hospitals, diagnostic centers etc. The HRP enables healthcare providers to become HIPs or HIUs and meet their obligations of sharing and securely maintaining health records of patients digitally. HRPs offer long term storage of health records on behalf of a HIP. For example, a hosted lab information management system provider (LIMS) may update their software to become a ABDM compatible Health Repository Provider. Any lab using this hosted LIMS software can rapidly become a HIP by adopting the software.

The ABDM sandbox hosts a reference HRP -- *You can play with it at* [https://emrsbx.abdm.gov.in](https://emrsbx.abdm.gov.in)

## What is an HIU?
An HIU (Health Information User) is an entity that wants access to digital health information from HIPs, in order to provide services to the patient to 
whom the information belongs. An HIU can be a hospital, clinic, healthcare technology company, organizations working on health analytics, insurers, medical 
researchers, government entities etc. These HIUs will be able to request for health records of a patient, and upon obtaining the patient’s digital consent, obtain a copy of the patients records and use them for the time period consented by the user.  

## What is a HIE-CM?
HIE-CM is Healthcare Information Exchange - Consent Manager. This is the key ABDM building block that enables managing consents related to user's personal health data and supports exchange of interoperable health data across ecosystem players who want to be HIPs and HIUs.

The architecture is designed to support multiple HIE-CMs to operate in the network. Each HIE-CM is referred to by a domain. NHA operates 2 HIE-CMs currently. A Sandbox HIE-CM with the domain @sbx and a production HIE-CM with the domain @abdm.  

## What is an ABHA address?
In order to manage their personal health records, users must first create an account on a HIE-CM -- called their Ayushman Bharath Health Account (ABHA) addresses. This looks like sandeep321@abdm and is also called as PHR Address. The @abdm tells us which HIE-CM is responsibile for this address.

Users can create an ABHA address by downloading a PHR mobile application or a portal provided by the HIE-CM. Use [phr.abdm.gov.in](https://phr.abdm.gov.in) to create a new ABHA address 

{{% notice%}}
Users can create an ABHA addresses in one of two ways:
1.  Using self declared information - This requires Name, Year of Birth gender along with a mobile number or email 
2.  Using an ABHA Number - This requires users to first create an ABHA number with strong KYC 

{{% /notice %}}
Users can start with a self declared ABHA address and later link it to an ABHA number 

While users are allowed to create more than one ABHA address, ABDM encourages every induvidual to have only ONE ABHA address. The process of obtaining an ABHA address is designed to ensure that users don't accidentally create multiple addresses

{{% icon icon="user-check" %}} *Try it out* - Create an ABHA address that you can use on the ABDM sandbox at [phrsbx.abdm.gov.in](https://phrsbx.abdm.gov.in). This will create an ABHA address on the @sbx HIE-CM hosted within the sandbox 

## What is an ABHA Number?
ABHA number is a *14 digit number* that is unique (only one per person) issued only after a strong KYC. You can link a PHR address with an ABHA number ABHA is a core building block of the ABDM ecosystem and integrates with several other systems to provide online KYC including Aadhaar, Driving licence and PAN 

You can obtain an ABHA by signing up at [https://abha.abdm.gov.in](https://abha.abdm.gov.in)

ABHA numbers are extremely important for helping those who use feature phones or do not use a phone to create their personal health records. ABHA numbers are issued in assisted mode extensively by all Government health programs. Each of these ABHA numbers also issues a PHR address on the @abdm HIE-CM. They look like <14digitabhano>@abdm. Government programs link any health records they create to this ABHA address.

*You can play around with the sandbox instance of the ABHA building block at* [https://abhasbx.abdm.gov.in](https://abhasbx.abdm.gov.in)

## What is a PHR application? 
Personal Health Record Applications are software service providers who offer front ends to individuals and enable them to create a ABHA address, discover and link health records from various HIPs, allow users to view their records, offer long term storage of records, upload users health records and share records on the ABDM network. PHR Apps work closely with the HIE-CM and provide a front end for HIE-CM actions like viewing and granting consents. 
(Note: That PHR Apps now subsume the entity type termed Health Lockers in earlier version of the HIP/HIU guidelines) 

*You can play around with the sandbox instance of the ABHA PHR app at*  [https://phrsbx.abdm.gov.in](https://phrsbx.abdm.gov.in)

## How does a HIE-CM create a longitudinal Health record 
The PHR architecture is inline with the concepts described in the Niti Aayog National Health Stack (NHS) strategy and the National Digital Health Blueprint documents.

ABDM is implemented as a Federated Architecture, where data is kept by the entity that generates the health data. Only a link called a *care context* is added to the PHR address. The HIE-CM is designed to be data blind, ie it does not know any details of the health records that are linked with the PHR address and the architecture ensures that any exchange of health data does not pass through the HIE-CM. 

The architecture is also fully aligned with the upcoming Data Protection Bill. The MietY consent framework and DEPA architecture is used to ensure that any data shared is only with a fully structured consent artifact. This design should ensure that any health facility using a ABDM compliant software will automatically be compliant to the Data protection bill. 
![How HIE-CM builds a PHR ](../hie_cm_linking.png)

{{% notice%}}
The Architecture ensures that there is 
- No central data repository
- Your PHR Address only holds links
- Each Health record is held by Health Facility that generated the record
- Health facilities that become HIPs collect & save your PHR address during registration
- HIP / HRPs notify or link new health records with your PHR address 
- HIP / HRPs share a copy of the linked record after verifying user consent
- Patient can get a copy of the records and view it using a PHR app
- PHR apps act as repositories that hold the health records long term for the user
- Patients can also upload records by scanning them or from their wearables via PHR apps 
- Only HIPs that are part of the Health Facility Registry can link health records with a PHR address
{{% /notice%}}

## Sharing Health Records With Consent

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
autonumber
participant hiu as Health Facility HIU
participant hiecm as HIE-CM
actor user as User via PHR App
participant hrp as Health Facility HRP/HIP
actor user
Note over hiu : Hospital would like to access medical history with consent
Note over hrp : Health Repository Providers holding user data
hiu->>hiecm: Sends consent request to ABHA address(user)
hiecm->>user: Presents consent request to user
user->>hiecm: Users grants consent
hiecm->>hiu: Signed consent from user
hiu->>hiecm: Request data with signed  consent
hiecm->>hrp:  Request HRP to Share data with HIU after verifying consent
hrp->>hiu: Encrypted health data in FHIR format
{{< /mermaid >}}

- When any HIU wants to access records linked with a PHR address, it initiates a consent request with the HIE-CM
- The consent request consists of the purpose for which health records are being sought, why type of records are being sought, from what time period and how long will the HIU like to retain these records
- HIE-CM forwards the request to the user who can view the request on their PHR app and decide what he actually wants to share when he grants the consent
- User's can also decide to revoke the consent anytime after it is granted
- If the user grants the consent, the HIE-CM shares a signed consent artificat with the the requesting HIU
- The HIU can now request for data for a PHR address along with the signed consent artificat
- The HIE-CM forwards the request to all HRPs that are holding the linked data 
- The HRPs verify the consent and push the data to the HIU
- Data has to be in the specified FHIR format to achieve interoperability 
- Data is encrypted using a method that ensures only the requesting HIU can decrypt the data 

 ## The ABDM Gateway 
Gateway is the hub that mediates and connects HIE-CMs, Health Repository Providers and HIUs in the network. Its primary job is to allow for discovery, routing in the network. The gateway does the following:

- Connects and validates the HIE-CMs and health repositories (servicing HIUs and HIPs) to the network.
- Enables routing of information.
- Authenticates connected systems within the PHR network (provides a signed authentication token for further communication). 
The entire PHR framework including the gateway communicates via asynchronous APIs over HTTPs channel.

The following figure provides a view of how the Gateway fits in with other components 
![ABDM digital health architecture](/abdm-docs/img/ABDM_digital_health_architecture.png)

## Experience PHR in action using the ABDM sandbox
ABDM provides a sandbox environment with core essential services that enable integrators who want to become HIPs/HIUs/HRPs or PHR apps build and test their integration. 

{{% icon icon="tasks" %}} Try out the following 

1. Create a PHR address on the sandbox from [https://phrsbx.abdm.gov.in/](https://phrsbx.abdm.gov.in/)
2. Use [EMRSBX](https://emrsbx.abdm.gov.in/) to register your PHR address and link it with a new health record 
3. Download and login to the Sandbox PHR app with your new PHR address {{% button href="https://play.google.com/store/apps/details?id=in.ndhm.phr&hl=en_IN&gl=US&pli=1" style="note" icon="download" %}}Download ABHA App{{% /button %}}
4. Provide consent and view the health record you linked via EMRSBX
5. Try adding your COVID vaccination record from CoWIN to your PHR address 

## Other relevant documents
1. [National Digital Health Blueprint](https://abdm.gov.in:8081/uploads/ndhb_1_56ec695bc8.pdf)
2. [National Health Stack](https://abdm.gov.in:8081/uploads/NHS_Strategy_and_Approach_1_89e2dd8f87.pdf)
3. [Electronic Consent Framework](https://dla.gov.in/sites/default/files/pdf/MeitY-Consent-Tech-Framework%20v1.1.pdf)

