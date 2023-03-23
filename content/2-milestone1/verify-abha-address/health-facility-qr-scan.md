+++
title = "By Scanning Health Facility QR Code"
date = 2023-03-16T09:30:25+05:30
weight = 1
chapter = true
pre = "<b>2.3.1 </b>"
+++

# By Scanning Health Facility QR Code

## Functionality Overview

Patients can **scan a Health Facility QR code** pasted at the facility registration counter on their ABHA application. 

The User/Patient can share their basic KYC information with the Health Facility (HMIS/LIMS) by scanning the QR Code using the ABHA application. This enables the user/patients to complete the seamless profile share during their visit.

*The authenticity of the profile information is verified by the HIE-CM internally before sharing the data with the Health Facility and before generating and further adding a linking token (Validity of 6 Months) along with the payload which can be used to link the health records through the HIP-initiated Linking service.*

![Scan HIP QR Code](../scan-hip-qr.png)

## Steps to scanning the QR Code:

1. Patient must have an ABHA app and have a valid ABHA address
2. Hospital must **generate a Health Facility QR code** and display it at the registration counter
3. Patient can then scan the QR code from his phone camera or his ABHA application
	- *If scanned from phone camera* -- The list of installed PHR apps is shown on the phone. The user can select any of the applications.
	- *If scanned from within the PHR app*, the app will call the share-profile API to the Health Facility.
4. The Health Facility will verify this is a registered healthcare provider and identify the HRP linked to this HIP in the ABDM registry.
5. The Gateway will call the share-profile API on the callback URL registered for this Health Facility
6. The HRP software must create a screen to display all the scanned profiles for a (counter) code
7. The operator (at the counter) should be able to select a shared profile and perform a fast user registration.

*Note: Remember to correctly handle this for both new and returning patients*


## Steps to create a QR code for your Health Facility:

Generate a QR code for the data in below format. You can use something like [Sample QR Generator](https://www.the-qrcode-generator.com/). 
*ABDM will shortly release a QR code generator that can be used.*

Your HIP ID is the same as the Health Facility Registry ID.
You must have linked this HIP ID to your HRP.

```json
{
    "hipId": "HFR1010342452",
    "code": "any information you want to get back with the scan, e,g counterId, Dept Id"
}
```

**Steps to open ABHA Application QR code scanner:**
- Go to ABHA Mobile Application **>** My Profile **>** Scan option on the top right
- Scan the QR code, the app should fetch details of QR code along with User profile details.
- Click on share which will make Health Facility call the expected API on HIP side.
- The successful message would be shown on application once the on-share callback is given.


## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Scan Health Facility QR Code to verify ABHA Address
actor User with PHR App
User with PHR App->>ABDM Sandbox Gateway:User scans the Health Facility QR code
ABDM Sandbox Gateway->>HRP:POST/v3/hip/patient/profile/share
HRP->>ABDM Sandbox Gateway:POST/v3/hip/patient/profile/on-share
{{< /mermaid >}}


## Test Cases:

Applicable | Test Title | Test Summary | Optional or Mandatory | Test Scenario | API Sequence | Expected Result | Actual Result
| ------| ----------- | ----------- | ----- | ------------------- | ------- | --------- | --------- |
VRFY_ABHA_01 - EMR/HMIS verifying ABHA | ABHA verification during patient registration using ABHA QR code | ABHA verification during patient registration. Health Provider scans the ABHA QR Code shown by the patient in PHR application. | Mandatory | EMR/HMIS scans the patients ABHA address QR code to get patient details into his system for registration. - Read contents of ABHA QR code. - Does demographic auth to verify the contents (KYC & LINK). - Save linking token. | {GATEWAY_HOST}/v0.5/users/auth/fetch-modes, {GATEWAY_HOST}/v0.5/users/auth/init, {GATEWAY_HOST}/v0.5/users/auth/confirm, {GATEWAY_HOST}/v0.5/users/auth/on-notify | EMR/HMIS system will save the ABHA Address as part of its patient's registration. EMR/HMIS system will save the Linking token | Details are fetched |
VRFY_ABHA_02 - EMR/HMIS sharing its facility QR code | Share Patient Profile with HIP by scanning HIP QR code (patient scans the HIP QR code) |Patient scans HIP QR code using their PHR mobile app|Mandatory|-QR code with HIP details is pasted at Health facility Registration desk. -Patients scans the HIP's QR code from PHR app. -Patient's ABHA address is shared with the Integrators system. -EMR/HMIS then does demographic auth to verify the contents (KYC & LINK) and saves linking token | {{CM_HOST}}/providers/{provider-id}, {{CM_HOST}}/patients/profile/share, {GATEWAY_HOST}/v0.5/users/auth/fetch-modes, {GATEWAY_HOST}/v0.5/users/auth/init, {GATEWAY_HOST}/v0.5/users/auth/confirm | 1. EMR/HMIS system will allow the patient to see & select from the list of profiles shared at the counter. 2. EMR/HMIS system will save ABHA Address as part of its patient's registration. 3. EMR/HMIS system will save Linking token |



