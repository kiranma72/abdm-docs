+++
title = "Support Deep links"
date = 2023-05-02T03:53:25+05:30
weight = 9
chapter = true
pre = "<b>5.9 </b>"
+++

# Support Deep Links

## Functionality Overview

Any mobile application that can display a user's personal health record (ABHA) under the Ayushman Bharat Digital Mission (ABDM) needs to adhere to the deep linking specification outlined in this document.

**User Flow:**

- Patient visits a health facility and registers by providing Name, DoB, Gender and Mobile. Patient does not share any ABHA Address with the facility.
- If the Health Facility is participating in ABDM, then it will notify ABDM when there is a new health record for this patient. Only the mobile number and the ID of the facility is notified. Facilities are identified by the facility’s HIPCODE. This can be obtained by registering the facility using the Health Facility Registry and linking the facility to a ABDM approved Health Repository Provider Software.
- ABDM will send an SMS to the user with a deep link.
- The content of the message will be:

(insert message content)

- Clicking on the link will show the list of all ABHA Mobile Applications that have cleared functional and security testing in the ABDM sandbox and have been production approved.

{{% badge %}}Note{{% /badge %}} The list of apps are presented in a random order each time the link is opened. The list of apps displayed is specific to the OS – Android or IOS

- Selecting an app will launch the app if already installed on the device or take the user to the play store (android) / app store (ios) to download the app. The deep link passed to the app in both scenarios contains the HIPCODE.
- The ABHA Mobile Application will help new users to register and create a ABHA Address using their name, date of birth, gender and mobile.
- The ABHA Mobile Application must recognize the invocation was via a Deep Link. It must initiate a Discovery request to the HIPCODE that was part of the deep link. The Discovery API is implemented by ABHA Mobile Applications to find health records at a health facility. It is important for the ABHA Mobile Application to guide the user to provide the same Name, DoB, Gender and Mobile number that was provided to the Health Facility. If there is any difference in this information, the record cannot be retrieved correctly.
- ABDM will forward the Discovery request from the ABHA Mobile Application to the participating Health Facility. The Discovery request consists of the ABHA Address (chosen by the user), Name, DoB, Gender and Mobile Number. The Health facility will search for any health records for this combination. If it finds a record it will respond to the ABHA Mobile Application with the available records listed in the form of care contexts.
- The ABHA Mobile Application should be able to display this to the user, link the care context to the ABHA Address, collect the appropriate consent from the user, fetch the health record(s) from the facility and display it to the user.

**Process to enable Deep Link support to your ABHA Mobile Application**

The ABHA Mobile Application must submit the following information to ABDM as part of Sandbox exit. Send an email to abdm.sandbox@nha.gov.in with the following details (eg here is AarogyaSetu)

- Name of the App: AarogyaSetu
- [Play Store Link](https://play.google.com/store/apps/details?id=nic.goi.aarogyasetu)
- [App Store Link](https://apps.apple.com/in/app/aarogyasetu/id1505825357)
- Android Intent URI: uhi://discover?hip='HIPCODE'
- iOS Intent URI: arogya://discover?hip='HIPCODE'
- Logo for your App: Share file as an attachment

Please note that for this version of the deep linking release there is some flexibility provided in the intent URI and you each ABHA Mobile Application can define its format. It is mandatory for all intent URIs to accept the HIPCODE. Here's a tip for implementors:

1. For [Android implementors](https://developer.android.com/training/app-links/deep-linking)
2. For [iOS implementors](https://developer.apple.com/ios/universal-links/)

**Demonstrating your Deep Link support during Sandbox Exit**

Get the team to configure your ABHA Mobile Application correctly on the sandbox implementation site at phrsbx.adbm.gov.in. if you are providing your application as an APK for sideloading note that only the “already installed” test case can be verified.

The EMRSBX application available at https://emrsbx.abdm.gov.in/ has been updated to support the deep linking flow.

- Login to EMRSBX.
- Register a new patient without providing a ABHA Address - Just use Name, DoB, Gender and a Mobile for the registration.
- Add a new Health record to this patient. You will get a notification SMS on the mobile with a deep link.
- The deeplink URI will point to phrsbx.adbm.gov.in/uhi/'HIPCODE'.
- App should behave correctly as defined in this document for both user cases.
	- New User - who downloads, installs and creates a ABHA Address
	- Already installed App user

When you launch the PHR app, it starts with a log-on page or the home page for a logged in user. ABDM requires the PHR app to start at a different page if invoked with a specific intent. This can be described in 2 scenarios:

**Scenario 1**
- QR Code at Facility is scanned using 3rd party camera app.
- This triggers a link (PHR | ABDM ) and lists the compatible PHR apps
- On selecting the PHR app, the PHR app is invoked with a specific intent. The App is expected to directly go to the share profile page pre-filled with the facility to share the profile

![scenario 1 deep link flow](/abdm-docs/img/deep-link-flow-s1.png)

**Scenario 2**
- User has not shared the ABHA address at the health facility. HF triggers an SMS notification with a deep link to the user’s mobile number when a new health record is created.
- The link looks like phr.abdm.gov.in/uhi/<hipcode>.
- On clicking the link, a list of compatible PHR applications is displayed.
- On selecting the PHR app, the app is invoked wiht the specific intent.
- The App is expected to go directly to the discovery and link page and pre-filled with the facility from which to discover recods.

![scenario 2 deep link flow](/abdm-docs/img/deep-link-flow-s2.png)

## Test Cases

**Deep Link Flow** : Send SMS to patient mobile to initiate record linking and fetching in PHR app

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | In case patient visits the health facility and do not provide the ABHA address for linking of health records. Then, ABDM compliant health facility will notify ABDM when there is a new health record created of the patient. ABDM will send a deep link SMS is to the patient's mobile for fetching and viewing records in PHR app using User Initiated Linking Flow (Discovery Flow) | Patient visits a health facility and registers by providing Name, DoB, Gender and Mobile. Patient does not share any ABHA Address with the facility.
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | In case patient visits the health facility and do not provide the ABHA address for linking of health records. Then, ABDM compliant health facility will notify ABDM when there is a new health record created of the patient. ABDM will send a deep link SMS is to the patient's mobile for fetching and viewing records in PHR app using User Initiated Linking Flow (Discovery Flow) | If the Health Facility is participating in ABDM, then it will notify ABDM when there is a new health record for this patient. Only the mobile number and the ID of the facility is notified. Facilities are identified by the facility’s HIPCODE. This can be obtained by registering the facility using the Health Facility Registry and linking the facility to a ABDM approved Health Repository Provider Software.
3| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | In case patient visits the health facility and do not provide the ABHA address for linking of health records. Then, ABDM compliant health facility will notify ABDM when there is a new health record created of the patient. ABDM will send a deep link SMS is to the patient's mobile for fetching and viewing records in PHR app using User Initiated Linking Flow (Discovery Flow) | ABDM will send an SMS to the user with a deep link as shown below: Dear Madam/Sir, (facility name) is now participating in Ayushman Bharat Digital Mission (ABDM). Your report at this facility is now ready. See your record by clicking on on phr.abdm.gov.in/uhi/(hipcode) ABDM|NHA
4| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | In case patient visits the health facility and do not provide the ABHA address for linking of health records. Then, ABDM compliant health facility will notify ABDM when there is a new health record created of the patient. ABDM will send a deep link SMS is to the patient's mobile for fetching and viewing records in PHR app using User Initiated Linking Flow (Discovery Flow) |Clicking on the link will show the list of all ABDM compliant PHR applications.

**Post clicking on deep link by patient** 

Use Case 1: In case ABDM compliant PHR application is not installed in PHR app, then user is redirected to download and install it from play store/app store."

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | Post clicking on deep link by patient| Check that, if no ABDM compliant PHR application is installed in phone - Navigate patient to play store / app store to install the selected PHR application from the list of all ABDM compliant PHR applications. 
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | Post clicking on deep link by patient| Check that, post installing the PHR app. New user is able to create the ABHA address and Password by providing basic details such as Nma, DoB, Gender, Mobile No., Address 


Use Case 2: In case ABDM compliant PHR application is already installed in PHR app, then app will directly launch and initiate the User Initiated Linking (Discovery Flow)

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | Post clicking on deep link by patient| Check that selected PHR app from the list of all ABDM compliant PHR app's is launched successfully. 
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | Post clicking on deep link by patient| Check that post launch, PHR app initiates the discovery request with HIP where patient health records were created


## API Sequence Diagram


## API Collection

