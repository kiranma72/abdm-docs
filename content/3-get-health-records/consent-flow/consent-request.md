---
title: "Consent Request"
date: 2022-06-21T12:53:25+05:30
weight: 1
draft: false
---



# Creation of Consent Request

## Overview of the functionality
 - From an HIU perspective, the flow begins when the HIU (e.g., a Doctor at a Hospital) requests consent to view the patient’s data.
 - Upon receipt of such a request from Gateway, CM acknowledges and sends back a consent request ID to the HIU via the gateway.
 - The CM then notifies the patient that an HIU has made a consent request.
 - The patient can view the request details and choose to either grant consent or deny it.
 - Subsequently, the CM notifies the HIU requester of the patient’s consent or denial status via the gateway.


1. If the request is granted, the CM sends across the Ids of the consent artefacts that were created against the request, to the HIU.
2. If the request is denied, the CM simply notifies the HIU of the denial of the request.


## API Sequence

The following diagram explains the consent request creation flow of forwarding the request to the gateway so that gateway can forward it to respective CM

![Consention of Consent Request](./consent_request_creation.PNG)


## API Information Request Response


### 1. Generate the Gateway session

Bearer token is received as part of respose and should be passed a Authorization token for subsequent API calls.

**URL:** https://dev.ndhm.gov.in/gateway/v0.5/sessions

**Request:** POST  

**Body:**

```json
{
    "clientId": "your-clientID",
    "clientSecret": "your-clientSecret",
    "grantType": "client_credentials"
}
```

**Response:** 200   OK

```json
{
    "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJBbFJiNVdDbThUbTlFSl9JZk85ejA2ajlvQ3Y1MXBLS0ZrbkdiX1RCdkswIn0.eyJleHAiOjE2NTMzNjkyNTYsImlhdCI6MTY1MzM2ODY1NnR",
    "expiresIn": 600,
    "refreshExpiresIn": 1800,
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICIyMWU5NzA4OS00ZTcxLTQyNGEtOTAzYS1jOTAyMWM1NmFlNWYifQ.eyJleHAiOjE2NTMzNzA0NTYsImlhdCI6MTY1MzM2ODY1NiwianRpIjoi",
    "tokenType": "bearer"
}
```




### 2. Identify a patient

This API is meant for identify to patient given her consent-manager-user-id

**URL:** https://dev.abdm.gov.in/gateway/v0.5/patients/find

**Request:** POST

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

Access token which was issued after successful login with gateway auth server

- X-CM-ID string (header) :  sbx (or) abdm

Suffix-of-the-consent-manager

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-06-21T10:53:44.967Z",
  "query": {
    "patient": {
      "id": "hinapatel79@sbx"
    },
    "requester": {
      "type": "HIU",
      "id": "HIU_ID"
    }
  }
}

```

**Response:**

202 	Accepted





### 3. Callback API for patient/find

If a patient is found then patient.name contains the patients name. Otherwise, patient is not provided, and possibly error is raised for invalid requests Note in addition to the "Authorization" header, one of the following headers must be specified

specify X-HIU-ID if the requester is HIU (identified from /find requester.id)
specify X-HIP-ID if the requester is HIP (identified from /find requester.id)

**URL:** {HIU CALLBACK URL}/v0.5/patients/on-find

**Request:** POST

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

Access token which was issued after successful login with gateway auth server

- X-HIU-ID string (header) : your-HIU-ID

Identifier of the health information user to which the request was intended

- X-HIP-ID string (header) : your-HIP-ID

Identifier of the health information provider to which the request was intended

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-06-21T10:59:01.680Z",
  "patient": {
    "id": "hinapatel79@sbx",
    "name": "Hina Patel"
  },
  "error": null,
  "resp": {
    "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  }
}

```

**Response:**

202 	Accepted




### 4. Create consent request

Creates a consent request to get data about a patient by HIU user.

**URL:** https://dev.abdm.gov.in/cm/v0.5/consent-requests/init

**Request:** POST

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

Access token which was issued after successful login with gateway auth server

- X-CM-ID string (header) :  sbx (or) abdm

Suffix-of-the-consent-manager

**Body:**

```json
{
    "requestId": "{{$guid}}",
    "timestamp": "{{timestamp}}",
    "consent": {
        "purpose": {
            "text": "Self requested",
            "code": "CAREMGT",
            "refUri": "string"
        },
        "patient": {
            "id": "hinapatel79@sbx"
        },
        "hiu": {
            "id": "HIU_ID"
        },
        "requester": {
            "name": "Dr. Manju",
            "identifier": {
                "type": "REGNO",
                "value": "MH1001",
                "system": "https://www.mciindia.org"
            }
        },
        "hiTypes": [
            "OPConsultation",
            "Prescription",
            "DischargeSummary",
            "DiagnosticReport",
            "ImmunizationRecord",
            "HealthDocumentRecord",
            "WellnessRecord"
        ],
        "permission": {
            "accessMode": 
                "VIEW",
            "dateRange": {
                "from": "2022-06-21T11:05:00.442Z",
                "to": "2022-06-21T11:05:00.442Z"
            },
            "dataEraseAt": "2022-06-21T11:05:00.442Z",
            "frequency": {
                "unit": "HOUR",
                "value": 1,
                "repeats": 1
            }
        }
    }
}

```

**Response:**

202 	Accepted





### 5. Response to consent request

Result of consent request creation for a patient. consentRequest.id represents the consentrequest id created by CM. The result must contain either consentRequest or the error caused.
Reasons for error may be Invalid references (e.g patient id, hiu id), purpose, hiTypes, ranges, persmission.

**URL:** {HIU CALLBACK URL}/v0.5/consent-requests/on-init

**Request:** POST

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

Access token which was issued after successful login with gateway auth server

- X-HIU-ID string (header) : your-HIU-ID

Identifier of the health information user to which the request was intended

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-06-21T11:13:31.921Z",
  "consentRequest": {
    "id": "f29f0e59-8388-4698-9fe6-05db67aeac46"
  },
  "error": null,
  "resp": {
    "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  }
}

```

**Response:**

202 	Accepted





### 6. Get consent request status

Get status of consent request done previously

**URL:** https://dev.abdm.gov.in/cm/v0.5/consent-requests/status

**Request:** POST

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

Access token which was issued after successful login with gateway auth server

- X-CM-ID string (header) :  sbx (or) abdm

Suffix-of-the-consent-manager

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-06-21T11:15:53.730Z",
  "consentRequestId": "string"
}

```

**Response:**

202 	Accepted




### 7. Result of consent request status

Result of consent request done previously. Status of request can be GRANTED, DENIED, EXPIRED. If the request was GRANTED, then

**URL:** {HIU CALLBACK URL}/v0.5/consent-requests/on-status

**Request:** POST

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

Access token which was issued after successful login with gateway auth server

- X-HIU-ID string (header) : your-HIU-ID

Identifier of the health information user to which the request was intended

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-06-21T11:16:58.583Z",
  "consentRequest": {
    "id": "<consent-request-id>",
    "status": "GRANTED",
    "consentArtefacts": [
      {
        "id": "<consent-artefact-id>"
      }
    ]
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

202 	Accepted



## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)

























