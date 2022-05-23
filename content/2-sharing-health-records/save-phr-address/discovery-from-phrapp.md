---
title: "Discovery from PHR Apps"
date: 2022-05-07T18:00:04+05:30
weight: 4
draft: false
---
## Discovery from PHR Apps : Overview of the functionality 
- Patient must have a PHR app and have a valid PHR address
- Patient LogIn to PHR app with Mobile/PHR Address/e-Mail/ABHA etc
- Patient makes a discovery request with verified identifiers along with name and demographic information 
- HIP revert with the Care Context detail  

<img width="184" alt="LoginwithPHR" src="https://user-images.githubusercontent.com/104073067/169785288-2d900932-7280-4a67-a8db-c84b0fcf462a.jpg">     <img width="184" alt="landingpage" src="https://user-images.githubusercontent.com/104073067/169791285-9e3ff444-2a1f-45a6-82a1-1feaa4f474fb.jpg"> <img width="184" alt="searchHIP" src="https://user-images.githubusercontent.com/104073067/169791298-731f4dcd-9f38-41a3-aff6-2669657699a1.jpg"> <img width="184" alt="linkedHIP" src="https://user-images.githubusercontent.com/104073067/169791288-8930b979-06f5-4245-8118-b64e793f7658.jpg"> <img width="184" alt="fetchrecrd" src="https://user-images.githubusercontent.com/104073067/169791277-da0db504-4efd-466f-839d-352e4f4ffee4.jpg"> <img width="184" alt="foundrecord" src="https://user-images.githubusercontent.com/104073067/169791281-a39409b9-4bee-491c-b7e0-038540119bc1.jpg"> <img width="184" alt="recvrecord" src="https://user-images.githubusercontent.com/104073067/169791295-08455588-73a5-4390-9862-280fef75cbfb.jpg"> <img width="184" alt="linksuccessfully" src="https://user-images.githubusercontent.com/104073067/169791291-a9f19188-2273-4c62-a6ea-f816c10f2dd6.jpg">



## Discovery of Patient’s information at the HIP

When the gateway calls an HIP system and requests for a particular patient’s records with a set of verifiable Ids, the process of information discovery begins. Upon receipt of the request, the HIP health repository reverts with a set of care context labels (in masked form). 

## Verify the patient and link the care context as requested by the patient 
This flow begins once a patient initiates a link request to the HIP to link the care context to the patient’s Consent Manager’s User ID. To enable the linking, the HIP system returns a link reference number along with the authentication type and its associated parameters.
The HIP system sends an OTP to the patient’s phone number. Note, the phone number for OTP communication from HIP may be the same as verified by the CM or maybe a different number that the patient has chosen as preferred mode of communication with HIP - meaning it's up to the HIP to choose the phone number it sends OTP to. The patient, via patient app, submits the OTP received from the HIP system within the stipulated time. If the patient is successfully authenticated by the HIP, the linking is now complete. The following flow diagrams details the flows that take place while linking to a health repository representing an HIP
Note : Post successful completion of discovery flow, its HIP’s prerogative to decide regarding implementation logic for saving the Verified identifier information (ABHA Address and ABHA number in case of KYC verified linking.

The following API sequence diagram details the flows that take place during patient information discovery from the HIP perspective
![API_discovery](https://user-images.githubusercontent.com/104073067/169794446-b42f13d5-3f35-4bb6-a558-59864fb3d2dd.jpg)
### 1. Discovery Request
Request for patient care context discover, made by Gateway intended for a specific HIP. It is expected that HIP will subsequently return either zero or one patient record with (potentially masked) associated care contexts

- At least one of the verified identifier matches
- Name (fuzzy), gender matches
- If YoB was given, age band(+-2) matches
- If unverified identifiers were given, one of them matches
- If more than one patient records would be found after aforementioned steps, then patient who matches most verified and unverified identifiers would be returned.
- If there would be still more than one patients (after ranking) error would be returned
- Intended HIP should be able to resolve and identify results returned in the subsequent link confirmation request via the specified transactionId
- Intended HIP should store the discovery results with transactionId and care contexts discovered for subsequent link initiation

**URL:** /v0.5/care-contexts/discover
**Request:** POST  
**HEADERS:**
- Authorization: Access token which was issued after successful login with gateway auth server, which will be sent by gateway to authenticate itself with API bridge
- X-HIP-ID: Identifier of the health information provider to which the request was intended.
**Request Body:**
```json
{
  {
  "requestId": "499a5a4a-7dda-4f20-9b67-e24589627061",
  "timestamp": "2022-05-23T10:30:58.871Z",
  "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "patient": {
    "id": "<patient-id>@<consent-manager-id>",
    "verifiedIdentifiers": [
      {
        "type": "MR",
        "value": "+919800083232"
      }
    ],
    "unverifiedIdentifiers": [
      {
        "type": "MR",
        "value": "+919800083232"
      }
    ],
    "name": "chandler bing",
    "gender": "M",
    "yearOfBirth": 2000
  }
}
```

**Response:**

202	Request Accepted

### 2. On-Discovery
Result of patient care-context discovery request at HIP end. If a matching patient found with zero or more care contexts associated, it is specified as result attribute. If the prior discovery request, resulted in errors then it is specified in the error attribute. Reasons of errors can be

- more than one definitive match for the given request
- no verified identifer was specified

**URL:** POST /v0.5/care-contexts/on-discover
**Request:**   
**HEADERS:**
- Authorization: Access token which was issued after successful login with gateway auth server, which will be sent by gateway to authenticate itself with API bridge. 
- X-CM-ID: Suffix of the consent manager to which the request was intended.(Should be the domain in the PHR Address - @sbx or @abdm)
**Request Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-23T10:38:59.874Z",
  "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "patient": {
    "referenceNumber": "string",
    "display": "string",
    "careContexts": [
      {
        "referenceNumber": "string",
        "display": "string"
      }
    ],
    "matchedBy": [
      "MR"
    ]
  },
  "error": {
    "code": 1000,
    "message": "string"
  },
  "resp": {
    "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  }
}```

**Response:**

202	Request Accepted

### 3. Link Patient's Care Contexts

Request from Gateway to links care contexts associated with only one patient

- Validate account reference number and care context reference number
- Validate transactionId in the request with discovery request entry to check whether there was a discovery and were these care contexts discovered or not for a given patient
- Before eventual link confirmation, HIP needs to authenticate the request with the patient(eg: OTP verification)
- HIP should communicate the mode of authentication of a successful request to Consent Manager
**URL:** /v0.5/links/link/init
**Request:** POST  
**HEADERS:**
- Authorization: JWT Sessions token (Access token which was issued after successful login with gateway auth server, which will be sent by gateway to authenticate itself with API bridge.)
- X-HIP-ID: Identifier of the health information provider to which the request was intended.
**Body:**
```json
{
  "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "timestamp": "2022-05-23T10:50:35.447Z",
  "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "patient": {
    "id": "hinapatel79@ndhm",
    "referenceNumber": "TMH-PUID-001",
    "careContexts": [
      {
        "referenceNumber": "string"
      }
    ]
  }
}
```

**Response:**

202	  Accepted


### 4. Response to patient's care context link request
Result of patient care-context link request from HIP end. This happens in context of previous discovery of patient found at HIP end, therefore the link requests ought to be in reference to the patient reference and care-context references previously returned by the HIP. The correlation of discovery and link request is maintained through the transactionId. HIP should have

- Validated transactionId in the request to check whether there was a discovery done previously, and the link request corresponds to returned patient care care context references
- Before returning the response, HIP should have sent an authentication request to the patient(eg: OTP verification)
- HIP should communicate the mode of authentication of a successful request
- HIP subsequently should expect the token passed via /link/confirm against the link.referenceNumber passed in this call

**URL:** /v0.5/links/link/on-init
**Request:** POST  
**HEADERS:**
- Authorization: Access token which was issued after successful login with gateway auth server, which will be sent by gateway to authenticate itself with API bridge
- X-HIP-ID: Identifier of the health information provider to which the request was intended.
**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-23T10:54:45.431Z",
  "transactionId": "a1s2c932-2f70-3ds3-a3b5-2sfd46b12a18d",
  "link": {
    "referenceNumber": "string",
    "authenticationType": "DIRECT",
    "meta": {
      "communicationMedium": "MOBILE",
      "communicationHint": "string",
      "communicationExpiry": "2019-12-30T12:01:55Z"
    }
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
202	 Accepted

