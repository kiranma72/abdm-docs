---
title: "Status Notification"
date: 2022-06-23T11:30:25+05:30
weight: 5
draft: false
---


#  Status Notification

## Overview of the functionality


## API Sequence


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





### 2. Notification sent by Consent Manager

Status (ACTIVE/DEACTIVATED/DELETED) will be sent to HIP. Note in addition to the "Authorization" header, one of the following headers must be specified

- X-HIU-ID if the requester is HIU
- X-HIP-ID if the requester is HIP

**URL:** {HIU CALLBACK URL}/v0.5/patients/status/notify

**Request:** POST

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

Access token which was issued after successful login with gateway auth server

- X-HIP-ID string (header) : your-HIP-ID

Identifier of the health information provider to which the request was intended

- X-HIU-ID string (header) : your-HIU-ID

Identifier of the health information user to which the request was intended

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-06-23T06:20:24.437Z",
  "notification": {
    "status": "DEACTIVATED",
    "patient": {
      "id": "hina@ncg"
    }
  }
}

```

**Response:**

202 	Accepted




### 3. Acknowledgment by HIP/HIU

This API is to be called by HIU/HIP bridge after receiving patient status (Activation/Reactivation/Deletion). In case of successfully receiving the notification "status" should sent as "OK" with no error.

**URL:**  https://dev.ndhm.gov.in/gateway/v0.5/patients/status/on-notify

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
  "timestamp": "2022-06-23T06:24:44.930Z",
  "acknowledgment": {
    "status": "OK"
  },
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








