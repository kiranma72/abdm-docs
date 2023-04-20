---
title: "Save Consent Notifications"
date: 2022-05-23
weight: 1
draft: false
---




### Overview of the functionality:

- HIU create a request to obtain a patient's consent to access  health information
- Consent request as HIU comes with a consent expiry time, after which you will not be able to access the patient's data.
- Patient grant or deny the consent request via PHR App
- The HIP/HRP receives the consent artefact after patients grants a request. Consent artefect saved in HIP/HRP end for future use.
- Approved/reject consent aretefect communicated to HIU


*Obtaining the patient’s consent for information sharing begins when the HIU system issues a consent request to the consent manager (HIE-CM) for the patient’s data. The patient can view the request details on his/her PHR App, and choose to either grant consent or deny it. The Consent Manager, notifies the HIU, and also sends a notification to the HIP/HRP of the patient’s consent if granted . HIP/HRP save that consent artefect for further use . Patient can also revoke the consent if desired.*


Following are the steps to notify the consent to HIP/HRP :

 **1:** HIU create a request to obtain a patient's consent to access her health information, as follows: 

Consent request may have follwoing details:
- User's consent manager ID
- Purpose of your consent request
- Details of who is requesting the health information
- The time period for which you require the patient's health documents. This information will enable your HIP to share the patient's health documents relevant to the required time period.
- Provide a list of the health information types for which you're requesting, such as clinical notes, examination data and so forth.

Consent request as HIU comes with a consent expiry time, after which you will not be able to access the patient's data.

 **2:** Patient Approved or reject the consent request via PHR App

 **3:** CM notify to HIP/HRP after patient grant approval . HIP/HRP save the consent artefact after patients grants a request. The consent artefact lets the HIP know what data needs to be shared, as detailed below:

- Patient's consent manager ID
- Purpose of data access consent
- Details of who is requesting the health information and of whom
- Health information types; the HIP needs to maintain details of what has been requested and what has been sent.

 **4:** Consent manager share the approved consent artifect with HIU.

Below is the diagram to explain the "notify the consent artefect" : 

![consentNotification](notify-consent.jpg)

## API Used :

Swagger link for above APIs - https://sandbox.abdm.gov.in/swagger/ndhm-hip.yaml 



###  Notify Consent

**End Point URL**: /v0.5/consents/hip/notify

**METHOD**: POST

**HEADERS**:
- Authorization: Access token which was issued after successful login with gateway auth server, which will be sent by gateway to authenticate itself with API bridge.
- X-HIP-ID: Identifier of the health information provider to which the request was intended.

**Request Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-06-09T06:32:59.560Z",
  "notification": {
    "status": "GRANTED",
    "consentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "consentDetail": {
      "schemaVersion": "string",
      "consentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "createdAt": "2022-06-09T06:32:59.560Z",
      "patient": {
        "id": "hinapatel79@ndhm"
      },
      "careContexts": [
        {
          "patientReference": "hinapatel79@hospital",
          "careContextReference": "Episode1"
        }
      ],
      "purpose": {
        "text": "string",
        "code": "string",
        "refUri": "string"
      },
      "hip": {
        "id": "string",
        "name": "TESI-HIP"
      },
      "consentManager": {
        "id": "string"
      },
      "hiTypes": [
        "OPConsultation"
      ],
      "permission": {
        "accessMode": "VIEW",
        "dateRange": {
          "from": "2022-06-09T06:32:59.560Z",
          "to": "2022-06-09T06:32:59.560Z"
        },
        "dataEraseAt": "2022-06-09T06:32:59.560Z",
        "frequency": {
          "unit": "HOUR",
          "value": 0,
          "repeats": 0
        }
      }
    },
    "signature": "Signature of CM as defined in W3C standards; Base64 encoded",
    "grantAcknowledgement": false
  }
}

```

**Response:**

202	Request Accepted

**Notes**

Notification of consents to health information providers consent request granted, consent revoked, consent expired. Only the GRANTED and REVOKED status notifications will be sent to HIP.

If consent is granted, status=GRANTED, then consentDetail contains the consent artefact details and signature is available.
If consent is revoked, then status=REVOKED, and consentId specifes which consent artefact is revoked.

###  On- Notify 
This API is called by HIP as acknowledgement to notification of consents, in cases of consent revocation and expiration.

**End Point URL**: /v0.5/consents/hip/on-notify

**METHOD**: POST

**HEADERS**:
- Authorization: Access token which was issued after successful login with gateway auth server, which will be sent by gateway to authenticate itself with API bridge.
- X-CM-ID: Suffix of the consent manager to which the request was intended.

**Request Body:**
```
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-06-09T06:42:34.297Z",
  "acknowledgement": {
    "status": "OK",
    "consentId": "<consent-artefact-id>"
  },
  "error": {
    "code": 1000,
    "message": "string"
  },
  "resp": {
    "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  }
}
```
**Response:**

202	Request Accepted
