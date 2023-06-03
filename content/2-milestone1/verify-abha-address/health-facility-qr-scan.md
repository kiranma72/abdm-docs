+++
title = "Scan Health Facility QR"
date = 2023-03-16T09:30:25+05:30
weight = 1
chapter = true
pre = "<b>2.2.1 </b>"
+++

# Scan Health Facility QR
|  Applicable To                             |   HMIS / LMIS (PVT)  |   Government Health App  | 
|-------------------------------|:----------------------:|:--------------------:|
|   Scan Health Facility QR                      |  {{% badge style="blue" %}}Mandatory{{% /badge %}}       |  {{% badge style="blue" %}} Mandatory{{% /badge %}}        | 


## Functionality Overview

Patients can **scan a Health Facility QR code** pasted at the facility registration counter on their PHR application. 

The User/Patient can share their profile with the HMIS/LIMS software used by the Health Facility by scanning a facility specific QR Code. This enables the user/patients to instantly register themselves, share their ABHA address and optionally obtain a token number from the facility. 

![Scan health facility QR Code](../scan-hf-qr.png)

**Steps to scanning the QR Code:**

1. User must have an PHR app and have a valid ABHA address
2. Hospital must **generate a Health Facility QR code** and display it at the registration counter
3. User can then scan the QR code from their phone camera or their PHR application
	- *If scanned from phone camera* -- The list of PHR apps is shown on the phone. The user can select any of the applications.
	- *If scanned from within a PHR app* - The app will obtain user consent and then call the share-profile API on HIE-CM. 
4. The HIE-CM will verify if this is a registered healthcare provider and identify the HRP linked to this Health Facility in the ABDM registry.
5. The Gateway will call the share-profile API on the callback URL registered by the HRP.
6. The HRP software must create a screen to display all the scanned profiles for a (counter) code.
7. The operator (at the counter) should be able to select a shared profile and perform a fast user registration.
8. The HRP software must correctly handle this for both new and returning patients

**Use Case 1: Scanned from within a PHR app**

![Use Case 1](../scan-hf-abha1.gif)

**Use Case 2: Scanned from phone camera **

![Use Case 2](../scan-hf-abha2.png)

**Steps to create a QR code for your Health Facility:**

1. Only ABDM compliant HFR registered facility/clinic and a doctor registered in HPR will be allowed to generate QR code in ABDM production.
2. The health facility can generate a printable QR code for its facility using the QR code generator built into the HFR application (is this deployed?)
3. For testing on the sandbox, Use [QR code generator](https://www.qr-code-generator.com/), put the HIP ID you linked with your client ID in the URL. 

{{% button style="info" %}}Try this out{{% /button %}} The content of the QR code is a URL in the following format:

https://phrsbx.abdm.gov.in/share-profile?hip-id=IN3410000260&counter-id=12345

- **Health Facility-ID:** Must be a valid Health Facility Registry ID issued by HFR. For Sandbox, this must be a HIP ID that is [linked with your client ID](/abdm-docs/1-basics/working_with_abdm_apis/#linking-the-hips--hius-id-for-a-client-id)
- **Counter-ID:**
	- Can be any facility-decided alphanumeric string. This field is passed back to the facility as part of the share-profile API call and can be used to identify the physical location where the QR code is present.
	- Given that the patient profile will be shared among all the counters and dynamic logic would be used for mapping the QR code to the counter, the counter number should be optional in payload for both QR code generation and scanning.
- **Other points:**
	- While scanning the QR code from an android device, the experience may differ based on android version, brand of the mobile and skin of the android OS. 
	- The experience may also differ based on the PHR application used to scan the QR code.

**Steps to open ABHA Application QR code scanner:**
- Go to Sandbox ABHA Mobile Application **>** My Profile **>** Scan option on the top right
- Scan the QR code, the app should fetch details of QR code along with User profile details.
- Click on share which will make Health Facility call the expected API on Health Facility side.
- The successful message would be shown on application once the on-share callback is given.

## Sample User Experience

Here's how the user journey looks on the Health Facility's side. These screen shots are from [Bahmni](/abdm-docs/1-basics/bahmni/). You can used the hip-id=Bahmni in the above URL to generate a QR code and try it out. 


![Scan Health Facility QR Code](/abdm-docs/img/scan-hf-qr.gif)


## Test Cases:

Applicable To | Test Summary | Test Scenario |
| --| ----------- | ------------------- |
{{% badge style="blue"%}}Mandatory{{% /badge %}}  EMR/HMIS verifying ABHA (SHARE_PATIENT_PROFILE_701) | Share Patient Profile when the User scans the QR code which is placed the facility premises | **1.** Log into PHR app. **2.** User will scan the QR code which is placed the facility premises. **3.** Post scanning, patient profile details are displayed including ABHA number, ABHA address, Name, Gender, DoB, Mobile No and Address. Below this consent language is displayed - "You consent to the above information to be shared with (Health facility Name). They can use this information for your registration and linking your health records and both Cancel/Share buttons are provided. **4.** Check that after clicking on "Share" button, user profile is successfully shared with the HIP and if user click on "Cancel" button then user profile is not shared with the HIP. **5.** User clicks on share and gets a token number. **6.** User clicks on ok and gets token number with validity of 30 minutes.

{{% notice title="API Versions" %}}

- **V3 API**
The V3 APIs provide a linking token at the time of share that must be saved by the HRP and used for HIP initiated linking
  - [Sequence Diagram for V3 API](#sequence-diagram-for-v3-api)
  - [API Information Request Response for V3](#api-information-request-response-for-v3)

- **V1.0 API**
The V1 APIs require the HRP to obtain a linking token via demographic auth as an additional step post profile share
  - [Sequence Diagram for V1 API](#sequence-diagram-for-v1-api)
  - [API Information Request Response for V1](#api-information-request-response-for-v1)

**Note:** V1.0 APIs are currently in production. V3 APIs are currently only available in sandbox
{{% /notice %}}


## Sequence Diagram for V3 API

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Scan Health Facility QR Code to verify ABHA Address
actor User with PHR App
User with PHR App->>HIE-CM:User scans the Health Facility QR code
HIE-CM->>HIP/HRP:POST/v3/hip/patient/profile/share
HIP/HRP->>HIE-CM:POST/v3/hip/patient/profile/on-share
{{< /mermaid >}}

## API Information Request Response for V3

**1. Profile Sharing** 

**BASE URLs:** The callback URL registered by the HRP
  
{{< swaggermin src="/abdm-docs/Yaml/HIE_CM_Profile_Share.yml" api="POST /{callback_url}/v3/hip/patient/profile/share$" >}}

**2. Acknowledgement for shared profile**

**BASE URLs:**
  - Sandbox Server URL: https://dev.abdm.gov.in/hiecm/api

  - Production Server URL: https://live.abdm.gov.in/hiecm/api

{{< swaggermin src="/abdm-docs/Yaml/HIE_CM_Profile_Share.yml" api="POST /{callback_url}/v3/app/patient/profile/on-share$" >}}

## Sequence Diagram for V1 API

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Scan Health Facility QR Code to verify ABHA Address using V1 API
actor User with PHR App
User with PHR App->>HIE-CM:User scans the Health Facility QR code
HIE-CM->>HIP/HRP:POST /v1.0/patients/profile/share
HIP/HRP-->>HIE-CM:POST /v1.0/patients/profile/on-share
note over HIE-CM,HIP: Use Demographics API to generate link token
{{< /mermaid >}}


## API Information Request Response for V1

**1. Profile Sharing** 

**BASE URLs:** The callback URL registered by the HRP

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v1.0/patients/profile/share$" >}}

**2. Acknowledgement for shared profile**

**BASE URLs:** https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v1.0/patients/profile/on-share$" >}}

**3. Link Token Generation**

For generating the link token use [demographics](/abdm-docs/2-milestone1/verify-abha-address/user-abha-qr-scan/#api-information-request-response) api.

{{% button style="tip" %}}  Try it out for yourself  {{% /button %}}

- Step 1: [Install ABHA Sandbox application](https://sandbox.abdm.gov.in/docs/phr_app) & Try it out 
- Step 2: [Register a callback URL](/abdm-docs/1-basics/working_with_abdm_apis/index.html#registering-your-callback-url)
- Step 3: Link a *fake* Health Facility ID to your client ID, [refer here](http://localhost:1313/abdm-docs/1-basics/working_with_abdm_apis/#linking-the-hips--hius-id-for-a-client-id)
- Step 4: Create QR code for your *fake* Health Facility ID
- Step 5: Scan QR code using ABHA sandbox Application
- Step 6: Get a share profile call from Sandbox on your callback URL
- Step 7: Respond with an on-share call using Postman
- Step 8: See the Token ID on your Sandbox ABHA application

