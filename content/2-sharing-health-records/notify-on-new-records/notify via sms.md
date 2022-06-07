---
title: "Notify via SMS"
date: 2022-05-30
weight: 1
draft: false
---


Whenever a new Health record (Prescription, Lab Report, etc) is created by the HRP and is ready to be shared with the patient, the HRP must check if there is a saved PHR address available for the patient. 

If there is no PHR address saved, the HRP must notify ABDM that there is now a new health record for the patient. The API only expects a mobile number. No information on the name of the patient or any details of the health record are part of the notification requirement.

ABDM uses this to help educate users that they can now access their health records from the health facility in a interoperable manner.

The expected User flow is given below :

![Deep Linking](../user-flow-deep-linking.jpg)

- Patient visits a health facility and registers by providing Name, DoB, Gender and Mobile. 
- Patient does not share any ABHA address with the facility.
- A new health record is ready to be shared with the patient
- The HRP calls the SMS notify API. Only the mobile number and the HIPCODE of the facility is part of the API.
- HIP Code is usually the same as the Health Facility Registry code of the health facility.  
- ABDM will send an SMS to the user with a deep link.
- The content of the message will be:

> Dear Madam/Sir,
>
>   __facility name__ is now participating in Ayushman Bharat Digital Mission (ABDM).
>    Your report at this facility is now ready. See your record by clicking on
>    on https://phr.abdm.gov.in/uhi/HIPCODE  
>
>    ABDM,NHA
>

-  Clicking on the link will show the list of all PHR Mobile Applications that are ABDM production approved
- The list of apps are presented in a random order each time the link is opened. 
- The list of apps displayed is specific to the OS – Android or IOS
- Selecting an app will launch the app if already installed on the device or take the user to the play store (android) / app store (ios) to download the app. 
- The deep link passed to the app in both scenarios contains the HIPCODE.
- The PHR Mobile Application will help new users to register and create a ABHA Address using their name, date of birth, gender and mobile.
- The PHR Application must recognize the invocation was via a Deep Link. It will initiate a Discovery request to the HIPCODE that was part of the deep link. It is important for the PHR Mobile Application to guide the user to provide the same Name, DoB, Gender and Mobile number that was provided to the Health Facility. If there is any difference in this information, the health record cannot be retrieved correctly.
- ABDM will forward the Discovery request from the PHR Application to the participating Health Facility. The Discovery request consists of the ABHA Address (chosen by the user), Name, DoB, Gender and Mobile Number. The Health facility will search for any health records for this combination. If it finds a record it will respond with the available records listed in the form of care contexts.
- The PHR Application should be able to display this to the user, link the care context to the ABHA Address, collect the appropriate consent from the user, fetch the health record(s) from the facility and display it to the user.

Following API must be be used by HRPs for the same -

#### 1. Call the notification API

**URL:**
**https://dev.abdm.gov.in/gateway/v0.5/patients/sms/notify2**

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

**Response**
202 Accepted 

#### 2. Check the call back to ensure it was successful

  
**URL:** 
**{HRP CALLBACK URL}/v0.5/patients/sms/on-notify**

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

## Ensure the flow works correctly 

Download the ABHA Mobile Application from the sandbox site at phrsbx.adbm.gov.in. 

- Create a new health record in your HRP for a user without a PHR address
- The SMS Notify API should be called by your HRP
- Verify that you get the deep link on your mobile phone
- Click on the link and launch the ABHA Mobile application. 
- Create or login with a PHR address that matches the patient that was registered in your HRP
- Verify that the ABHA application is now able to discover the record
- Note that you must have already implemented the discovery flow in yoru HRP. 

