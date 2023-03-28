+++
title = "Scan Health Facility QR"
date = 2023-03-16T09:30:25+05:30
weight = 1
chapter = true
pre = "<b>2.3.1 </b>"
+++

# Scan Health Facility QR

## Functionality Overview

Patients can **scan a Health Facility QR code** pasted at the facility registration counter on their ABHA application. 

The User/Patient can share their basic KYC information with the Health Facility (HMIS/LIMS) by scanning the QR Code using the ABHA application. This enables the user/patients to complete the seamless profile share during their visit.

![Scan health facility QR Code](../scan-hf-qr.png)

**Steps to scanning the QR Code:**

1. Patient must have an ABHA app and have a valid ABHA address
2. Hospital must **generate a Health Facility QR code** and display it at the registration counter
3. Patient can then scan the QR code from his phone camera or his ABHA application
	- *If scanned from phone camera* -- The list of installed PHR apps is shown on the phone. The user can select any of the applications.
	- *If scanned from within the PHR app*, the app will call the share-profile API to the Health Facility.
4. The Health Facility will verify this is a registered healthcare provider and identify the HRP linked to this Health Facility in the ABDM registry.
5. The Gateway will call the share-profile API on the callback URL registered for this Health Facility
6. The HRP software must create a screen to display all the scanned profiles for a (counter) code
7. The operator (at the counter) should be able to select a shared profile and perform a fast user registration.

*Note: Remember to correctly handle this for both new and returning patients*

**Use Case 1: ABDM compliant ABHA application is already installed in user’s phone**

*insert image slider for UX, awaiting Kiran to share the refernce*

**Use Case 1: No ABDM compliant ABHA application is installed**

*insert image slider for UX, awaiting Kiran to share the refernce*

**Steps to create a QR code for your Health Facility:**

1. Only ABDM compliant HFR registered facility/clinic and a doctor registered in HPR will be allowed to generate QR code from ABDM system with ABDM branding guidelines
2. ABDM logo unit must be placed at the center of the ABDM QR to indicate that the QR scanning functionality has been routed through ABDM
3. The health facility can generate a printable QR code for its facility using the QR code generator application at this link

![Health Facility QR code generator](../hfr-qr-code-generator.png)

**QR Code Content**

{{% button href="https://phrsbx.abdm.gov.in/share-profile?hip-id=IN3410000260&counter-id=12345" style="info" %}}Try out the QR Code Generator here{{% /button %}}

- **Health Facility-ID:** Must be a valid Health Facility Registry ID issued by HFR
- Counter-ID:
	- Can be any facility decided alphanumeric string. This field is passed back to the facility as part of the share-profile API call and can be used to identify the physical location where the QR code is present.
	- Given that the patient profile will be shared among all the counters and dynamic logic would be used for mapping the QR code to the counter,the counter number should be optional in payload for both QR code generation and scanning
- **URL:**
	- This URL is static and this needs to be dynamic
	- This URL needs to change to some generic URL aligned with QR code action which is easily understood by user.
- **Other points:**
	- While scanning the QR code from an android device, the experience may differ based on android version, brand of the mobile and skin of the android OS. Tech team to also provide list of exceptions, if any along with the list of devices/operating system on which this experience will not work or will have limited experience.
	- The experience may also differ based on the QR scanning application from which the user is scanning the QR code.

**Steps to open ABHA Application QR code scanner:**
- Go to ABHA Mobile Application **>** My Profile **>** Scan option on the top right
- Scan the QR code, the app should fetch details of QR code along with User profile details.
- Click on share which will make Health Facility call the expected API on Health Facility side.
- The successful message would be shown on application once the on-share callback is given.


## Test Cases:

Applicable To | Test Summary | Test Scenario |
| --| ----------- | ------------------- |
{{% badge style="blue"%}}Mandatory{{% /badge %}}  EMR/HMIS verifying ABHA (SHARE_PATIENT_PROFILE_701) | Share Patient Profile when the User scans the QR code which is placed the facility premises | 1. Log into PHR app. 2. User will scan the QR code which is placed the facility premises. 3. Post scanning, patient profile details are displayed including ABHA number, ABHA address, Name, Gender, DoB, Mobile No and Address. Below this consent language is displayed - "You consent to the above information to be shared with (Health facility Name). They can use this information for your registration and linking your health records and both Cancel/Share buttons are provided. 4.Check that after clicking on "Share" button, user profile is successfully shared with the HIP and if user click on "Cancel" button then user profile is not shared with the HIP. 5. User clicks on share and gets a token number. 6. User clicks on ok and gets token number with validity of 30 minutes.

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

## API Information Request Response 

**1. Profile Sharing** 

**BASE URLs:**
  - Sandbox Server URL: https://dev.abdm.gov.in/hiecm/api
  
  - Production Server URL: https://live.abdm.gov.in/hiecm/api

{{< swaggermin src="/abdm-docs/Yaml/HIE_CM_Profile_Share.yml" api="POST /{callback_url}/v3/hip/patient/profile/share$" >}}

**2. Acknowledgement for shared profile**

**BASE URLs:**
  - Sandbox Server URL: https://dev.abdm.gov.in/hiecm/api

  - Production Server URL: https://live.abdm.gov.in/hiecm/api

{{< swaggermin src="/abdm-docs/Yaml/HIE_CM_Profile_Share.yml" api="POST /{callback_url}/v3/app/patient/profile/on-share$" >}}


{{% button style="tip" %}}  Try it out for yourself  {{% /button %}}

- Step 1: [Install ABHA Sandbox application](https://sandbox.abdm.gov.in/docs/phr_app) & Try it out 
- Step 2: Register a callback URL
- Step 3: Link a *fake* Health Facility ID to your client ID, and [add link here]( https://kiranma72.github.io/abdm-docs/1-basics/working_with_abdm_apis/index.html#registering-your-callback-url)
- Step 4: Create QR code for your *fake* Health Facility ID
- Step 5: Scan QR code using ABHA sandbox Application
- Step 6: Get a share profile call from Sandbox on your callback URL
- Step 7: Respond with an on-share call using Postman
- Step 8: See the Token ID on your Sandbox ABHA applicatioin

