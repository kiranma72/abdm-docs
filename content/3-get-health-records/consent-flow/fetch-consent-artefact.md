---
title: "Fetching the Consent artefact"
date: 2022-06-22T11:07:25+05:30
weight: 3
draft: false
---



# Fetching the Consent artefact

## Overview of the functionality

 - Once the patient grants consent to the HIU, the CM notifies the HIU system of the consent grant via the gateway.
 - If the patient grants for multiple HIPs, then multiple consent artefacts are generated - one for each HIP.
 - The HIU now first fetches all the consent-artefacts that were generated for its request.

## API Sequence

The following diagram explains the Fetching of Consent artefact

![Consention of Consent Request](./fetching_the_consent_artefact.PNG)


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

**Response:** 

200   OK

```json
{
    "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJBbFJiNVdDbThUbTlFSl9JZk85ejA2ajlvQ3Y1MXBLS0ZrbkdiX1RCdkswIn0.eyJleHAiOjE2NTMzNjkyNTYsImlhdCI6MTY1MzM2ODY1NnR",
    "expiresIn": 600,
    "refreshExpiresIn": 1800,
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICIyMWU5NzA4OS00ZTcxLTQyNGEtOTAzYS1jOTAyMWM1NmFlNWYifQ.eyJleHAiOjE2NTMzNzA0NTYsImlhdCI6MTY1MzM2ODY1NiwianRpIjoi",
    "tokenType": "bearer"
}
```

### 2. Get consent artefact


**URL:** https://dev.ndhm.gov.in/gateway/v0.5/consents/fetch

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
  "timestamp": "2022-06-22T06:51:39.024Z",
  "consentId": "string"
}

```

**Response:**

202 	Accepted



### 3. Result of fetch request for a consent artefact

Must contain either consentDetail or error. Possible reason of errors are

consentId passed through /fetch is invalid

**URL:** {HIU CALLBACK URL}/v0.5/consents/on-fetch

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
  "timestamp": "2022-06-22T06:54:04.799Z",
  "consent": {
    "status": "GRANTED",
    "consentDetail": {
      "schemaVersion": "string",
      "consentId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "createdAt": "2022-06-22T06:54:04.799Z",
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
        "id": "string"
      },
      "hiu": {
        "id": "string"
      },
      "consentManager": {
        "id": "string"
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
        "OPConsultation"
      ],
      "permission": {
        "accessMode": "VIEW",
        "dateRange": {
          "from": "2022-06-22T06:54:04.799Z",
          "to": "2022-06-22T06:54:04.799Z"
        },
        "dataEraseAt": "2022-06-22T06:54:04.799Z",
        "frequency": {
          "unit": "HOUR",
          "value": 0,
          "repeats": 0
        }
      }
    },
    "signature": "Signature of CM as defined in W3C standards; Base64 encoded"
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
