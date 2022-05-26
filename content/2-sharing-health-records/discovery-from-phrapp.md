---
title: "Support Discovery of Records"
date: 2022-05-23
weight: 2
draft: false
pre: "<b>2.2 </b>"
---

## Overview of the functionality 


- User must have a PHR app and have a valid PHR address
- User is logged in into their PHR App 
- User searches for a health facility which they have visited in the past. 
- The health facility must be a HIP (part of facility registry) and linked with a HRP for discovery to be supported 
- User makes a discovery request via PHR app - ie requests the HIP to find any health records in their name
- User shares details from their PHRAddress ie Name, Date of birth gender, verified mobile no with the HIP / HRP
- The HRP is expected to search its database for any records that match this patient. 
- If there is a match, the HRP returns with the Care Context details for the records available
- If there is no match, the HRP returns an error
- The User can now request to link the records (care contexts) with their PHR address 
- The HRP will perform a validation by sending an OTP to the registered mobile
- If the authentication succeeds, the care contexts are linked to the PHR address
- The HRP must save this PHR address in its database and automatically link new records in the future. 



## Discovery & Linking Flow in ABHA PHR App

![login](../discovery-process-abha-app.png)

## API Sequence

![API_discovery](../discovery-api-seq.jpeg)

Swagger link for above APIs - https://sandbox.abdm.gov.in/swagger/ndhm-hip.yaml 



### 1. Discovery Request

Developers can search for the facility name they registered for their HRP using the ABDM PHR Sandbox App. The Discovery request will be sent to the HRP callback Url registered with the sandbox.

**URL**: {HRP_CALLBACK_URL}/v0.5/care-contexts/discover

**METHOD**: POST

**HEADERS**:
- Authorization: Gateway JWT Token
- X-HIP-ID: HIP (health facility ID) selected by user in PHR APP

**Request Body:**
```json
{
  "patient": {
    "id": "kiranma@sbx",
    "name": "Kiran Anandampillai",
    "gender": "M",
    "yearOfBirth": 19XX,
    "verifiedIdentifiers": [
      {
        "type": "MOBILE",
        "value": "98XXXXX767"
      },
      {
        "type": "NDHM_HEALTH_NUMBER",
        "value": "42-7175-8604-4553"
      },
      {
        "type": "HEALTH_ID",
        "value": "kiranma@sbx"
      }
    ],
    "unverifiedIdentifiers": []
  },
  "requestId": "46c1db89-03b2-4bc7-b841-cd413b1dfd4f",
  "timestamp": "2022-05-25T01:09:02.330549",
  "transactionId": "f8b66886-1df2-47a3-9939-9504e8e31b32"
}
```

**Response:**

202	Request Accepted

**Notes**

When a HRP recieves a discovery request, it is expected to search its health record database for a match and correctly implement the following logic

![Discovery Logic](../discovery-logic-hrp.png)


- Start by matching the HEALTH_ID (PHR Address). If you cannot find that, try to match by mobile number 
- If no records are found, check for other "unverified identifiers" if shared by the user. Users can share say a patient ID issued by the healthcare provider 
- If there are patient records matched, ensure exact match for Gender and a (+-2 years) for Year of Birth
- Finally do an fuzzy match on Name. We recommend the **Levenshtein distance** algorithm for fuzzy matches
- You can to call the on-discover API with all the care contexts for the patient. You share share all records including old records.Read this understand how to organize health records into Care Contexts


### 2. On-Discovery
Result of patient care-context discovery request at HRP end. Remember to send back the transactionId recieved in the discover request

If a matching patient found with zero or more care contexts associated, it is specified as result attribute. If the prior discovery request, resulted in errors then it is specified in the error attribute. Reasons of errors can be

- more than one definitive match for the given request
- no verified identifer was specified

**URL**: https://dev.abdm.gov.in/gateway/v0.5/care-contexts/discover

**METHOD**: POST

**HEADERS**:
- Authorization: Session Token using Client ID
- X-CM-ID: sbx or adbm. Must be the same as the domain shared in the HEALTH_ID

**Request Body:**

**Example1: Request matched a patient record**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-23T10:38:59.874Z",
  "transactionId": "f8b66886-1df2-47a3-9939-9504e8e31b32",
  "patient": {
    "referenceNumber": "DiscoveryRef-352341",
    "display": "Records found for Kiran Anandampillai",
    "careContexts": [
      {
        "referenceNumber": "HT1254323",
        "display": "Prescription from OPD Visit on 12-05-22"
      }, 
      {
        "referenceNumber": "HT1254324",
        "display": "Inpatient records from 16-05-22"
      } 
    ],
    "matchedBy": [
      "MR -- What goes here?" 
    ]
  }
  "resp": {
    "requestId": "46c1db89-03b2-4bc7-b841-cd413b1dfd4f"
  }
}
```

**Response:**

202	Request Accepted

** Notes ** 
Create a unique referenceNumber for this response like "DiscoveryRef-352341". Save the list of care-contexts shared against this reference in your HRP. The PHR app will display the care contexts shared by the HRP to the user. The user can decide which care contexts they would like to link with their PHR Address 


### 3. Link Patient's Care Contexts

Request from Gateway to links care contexts selected by the patient. The same transaction ID from the on-discover will be sent by the gateway

**URL:** {HRP_CALLBACK_URL}/v0.5/links/link/init

**Request:** POST  

**HEADERS:**
- Authorization: Gateway JWT Token
- X-HIP-ID: Health facility ID linked with this HRP

**Request Body:**

**Example:**
```json
{
  "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "timestamp": "2022-05-23T10:50:35.447Z",
  "transactionId": "f8b66886-1df2-47a3-9939-9504e8e31b32",
  "patient": {
    "id": "kiranma@sbx",
    "referenceNumber": "DiscoveryRef-352341",
    "careContexts": [
      {
        "referenceNumber": "HT1254323"
      },
     {
        "referenceNumber": "HT1254324"
      }
    ]
  }
}
```

**Response:**

202	  Accepted

** Notes ** 

The HRP is expected to perform the following validations before responding via the the on-init API call

- Validate the transactionId in the request is the same one for which the HRP has shared the care contexts
- Validate the Discovery reference number and care context reference numbers are what was shared earlier by HRP
- Ensure the PHR Address is the same as in the discovery request
- if validations are successful, The HRP is expected to perform an authentication before linking (eg: via SMS OTP)


### 4. Response to patient's care context link request

- Use the same transactionId from the init request and the link request corresponds to returned patient care care context references
- HRP is expected to send an OTP SMS message to the users mobile number (using its own SMS gateway) 

**URL:** http://dev.abdm.gov.in/v0.5/links/link/on-init

**Request:** POST  

**HEADERS:**
- Authorization: Session Token using Client ID
- X-CM-ID: sbx or adbm. Must be the same as the domain shared in the HEALTH_ID

**Request Body:**

**Example**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-23T10:54:45.431Z",
  "transactionId": "f8b66886-1df2-47a3-9939-9504e8e31b32",
  "link": {
    "referenceNumber": "DiscoveryRef-352341",
    "authenticationType": "DIRECT",
    "meta": {
      "communicationMedium": "MOBILE",
      "communicationHint": "OTP sent to mobile no 9845XXX767",
      "communicationExpiry": "2022-05-23T15:30:35.237Z"
    }
  }
  "resp": {
    "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  }
}
```

**Response:**
202	 Accepted

### 5. Token Submission from gateway for link confirmation

**URL:** {HRP_CALLBACK_URL}/v0.5/links/link/confirm

**Request:** POST  
**HEADERS:**
- Authorization: Gateway JWT Token
- X-HIP-ID: Health facility ID linked with this HRP

**Request Body:**

**Example:**

```json
{
  "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "timestamp": "2022-05-23T11:20:44.122Z",
  "confirmation": {
    "linkRefNumber": "DiscoveryRef-352341",
    "token": "345234"
  }
}
```

**Response:**

202	  Accepted

** Notes ** 

- The HRP must verify that the reference number was issued by it 
- The HRP must verify that the token matches the OTP it sent via SMS for this reference number
- If the above 2 match, the HRP is now expected to save the PHR address for this user against these health records
- The HRP is expected to maintain the list of care-contexts that are already linked
- The HRP can use the PHR address and auto-link newer records created by it 

### 6. Confirm linkage of care-contexts if token matches

**URL:** http://dev.abdm.gov.in/v0.5/links/link/on-confirm

**Request:** POST  

**HEADERS:**
- Authorization: Session Token using Client ID
- X-CM-ID: sbx or adbm. Must be the same as the domain shared in the HEALTH_ID

**Request Body:**

**Example:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-23T11:22:33.380Z",
  "patient": {
    "referenceNumber": "DiscoveryRef-352341",
    "display": "Linked Care contexts for Kiran Anandampillai",
    "careContexts": [
      {{
        "referenceNumber": "HT1254323",
        "display": "Prescription from OPD Visit on 12-05-22"
      }, 
      {
        "referenceNumber": "HT1254324",
        "display": "Inpatient records from 16-05-22"
      } 
    ]
  },
  "resp": {
    "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  }
}
```

**Response:**

202	 Accepted








## Postman + Curl Collection 

**Download the Postman Collection** [here](../Discover_Link_Flow.json)

**Download the Curls** [here](/abdm-docs/Curls/)






TODO:

- Document error responses for common errors 
- Add POSTMAN collection for testing
