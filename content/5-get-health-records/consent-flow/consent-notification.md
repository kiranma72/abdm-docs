---
title: "Consent Notification"
date: 2022-06-22T11:07:25+05:30
weight: 2
draft: false
---






# Patient Consent Notification from CM to HIU

## Overview of the functionality



## API Sequence

The following diagram explains the consent notification flow

![Consention of Consent Request](./consent_notification_from_CM_to_HIU.PNG)


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




### 2. Consent notification

Health information user will get notified about the consent request granted or denied, consent revoked, consent expired.

- For consent request grant, status=GRANTED, consentRequestId=<consent-request-id>, and consentArtefacts is an array of generated consent artefact Ids.
- For consent request expiry, status=EXPIRED, consentRequestId=<consent-request-id>
- For consent request denied, status=DENIED, consentRequestId=<consent-request-id>
- For consent revocation, status=REVOKED, consentArtefacts is an array of revoked consent artefact ids

**URL:** {HIU CALLBACK URL}/v0.5/consents/hiu/notify

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
  "timestamp": "2022-06-22T05:49:08.429Z",
  "notification": {
    "consentRequestId": "<consent-request-id>",
    "status": "GRANTED",
    "consentArtefacts": [
      {
        "id": "<consent-artefact-id>"
      }
    ]
  }
}

    
```

**Response:**

202 	Accepted


    
### 3. Call API for Consent notification

This API is called by HIU as acknowledgement to consent notifications, specifically for cases when consent is REVOKED or EXPIRED.

**URL:** https://dev.ndhm.gov.in/gateway/v0.5/consents/hiu/on-notify

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
  "timestamp": "2022-06-22T05:54:39.566Z",
  "acknowledgement": [
    {
      "status": "OK",
      "consentId": "<consent-artefact-id>"
    }
  ],
  "error": null,
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
