---
title: "Notify via SMS"
date: 2022-05-30
weight: 1
draft: false
---



#  SMS Notify - If the PHR address of the patient is not saved   #

ABDM plans to ensure that users are aware of which health facilities are participating in ABDM. HRPs are expected to notify ABDM whenever a new health record is created using this API.

The expected User flow is given below :

![Deep Linking](../USERFLOW–DEEPLINKING.jpg)

- Patient visits a health facility and registers by providing Name, DoB, Gender and Mobile. Patient does not share any ABHA address with the facility.
- If the Health Facility is participating in ABDM, then it will notify ABDM when there is a new health record for this patient. Only the mobile number and the HIP ID of the facility is notified. Facilities are identified by the facility’s HIPCODE. This can be obtained by registering the facility using the Health Facility Registry and linking the facility to a ABDM approved Health Repository Provider Software.
- ABDM will send an SMS to the user with a deep link.
- The content of the message will be:
```
 Dear Madam/Sir,
   <facility name> is now participating in Ayushman Bharat Digital Mission (ABDM).
    Your report at this facility is now ready. See your record by clicking on
    on phr.abdm.gov.in/uhi/<hipcode>
    
    ABDM,NHA
 ```
 
-  Clicking on the link will show the list of all ABHA Mobile Applications that have cleared functional and security testing in the ABDM sandbox and have been production approved.

**The list of apps are presented in a random order each time the link is opened. The list of apps displayed is specific to the OS – Android or IOS**

- Selecting an app will launch the app if already installed on the device or take the user to the play store (android) / app store (ios) to download the app. The deep link passed to the app in both scenarios contains the HIPCODE.
- The ABHA Mobile Application will help new users to register and create a ABHA Address using their name, date of birth, gender and mobile.
- The ABHA Mobile Application must recognize the invocation was via a Deep Link. It must initiate a Discovery request to the HIPCODE that was part of the deep link. The Discovery API is implemented by ABHA Mobile Applications to find health records at a health facility. It is important for the ABHA Mobile Application to guide the user to provide the same Name, DoB, Gender and Mobile number that was provided to the Health Facility. If there is any difference in this information, the record cannot be retrieved correctly.
- ABDM will forward the Discovery request from the ABHA Mobile Application to the participating Health Facility. The Discovery request consists of the ABHA Address (chosen by the user), Name, DoB, Gender and Mobile Number. The Health facility will search for any health records for this combination. If it finds a record it will respond to the ABHA Mobile Application with the available records listed in the form of care contexts.
- The ABHA Mobile Application should be able to display this to the user, link the care context to the ABHA Address, collect the appropriate consent from the user, fetch the health record(s) from the facility and display it to the user.


Following API must be be used by HRPs for the same -


**URL:**
**/v0.5/patients/sms/notify2**

**METHOD**: POST

**HEADERS**:
- Authorization: Session Token using Client ID
- X-CM-ID: sbx or adbm. Must be the same as the domain shared in the HEALTH_ID

**Request Body:**
```
  {
    "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
    "timestamp": "2022-02-08T10:48:02.530Z",
    "notification": {
      "phoneNo": "+91-9999999999",
      "hip": {
        "name": "Max Healthcare",
        "id": "DEMO_TEST_008"
      }
    }
  }  
  ```
  
  
**URL:** 
**/v0.5/patients/sms/on-notify**

**METHOD**: POST

**HEADERS**:
- Authorization: Session Token using Client ID
- X-CM-ID: sbx or adbm. Must be the same as the domain shared in the HEALTH_ID


If the SMS notification is successfully sent to the patient then "status" will be "ACKNOWLEDGED" with no error. If the SMS notification is failed then "status" will be "ERRORED" with error.

**Request Body:**
```
 {
    "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
    "timestamp": "2022-02-08T10:56:37.221Z",
    "status": "ACKNOWLEDGED",
    "error": {
      "code": 1000,
      "message": "string"
    },
    "resp": {
      "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    }
  }
```

## Demonstrating your Deep Link support during Sandbox Exit ##

Get the team to configure your ABHA Mobile Application correctly on the sandbox implementation site at phrsbx.adbm.gov.in. if you are providing your application as an APK for sideloading note that only the “already installed” test case can be verified.

The EMRSBX application available at https://emrsbx.abdm.gov.in/ has been updated to support the deep linking flow.

- Login to EMRSBX.
- Register a new patient without providing a ABHA Address - Just use Name, DoB, Gender and a Mobile for the registration.
- Add a new Health record to this patient. You will get a notification SMS on the mobile with a deep link.
- The deeplink URI will point to phrsbx.adbm.gov.in/uhi/'HIPCODE'.
- App should behave correctly as defined in this document for both user cases.
- New User - who downloads, installs and creates a ABHA Address
- Already installed App user
