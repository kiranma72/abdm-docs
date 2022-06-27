---
title: "Subscription Request Flow"
date: 2022-06-21T12:53:25+05:30
weight: 1
draft: false
---


# Creation of Subscription Request Flow

## Overview of the functionality
  - Subscription request against PHR address
  - Subscription Request appoval Notification to HIU
  - Whenever new data is available the HIU will be notified if there is an active subscription.


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



### 2. Create Request for Subscription


Creates a request for subscription. The subscription categories can be for care-contexts linkages or availability of data against existing care-contexts. Note that the requester must have HIU role.

**URL:** https://dev.abdm.gov.in/gateway/v0.5/subscription-requests/cm/init

**Request:** POST

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

Access token which was issued after successful login with gateway auth server

- X-CM-ID string (header) :  sbx (or) abdm

Suffix-of-the-consent-manager

**Body:**

```json
{
  "requestId": "499a5a4a-7dda-4f20-9b67-e24589627061",
  "timestamp": "2022-06-21T07:44:12.142Z",
  "subscription": {
    "purpose": {
      "text": "string",
      "code": "string",
      "refUri": "string"
    },
    "patient": {
      "id": "hinapatel79@sbx"
    },
    "hiu": {
      "id": "HIU_ID"
    },
    "hips": [
      {
        "id": "HIP_ID"
      }
    ],
    "categories": [
      "LINK"
    ],
    "period": {
      "from": "2022-06-21T07:44:12.142Z",
      "to": "2022-06-21T07:44:12.142Z"
    }
  }
}

```

**Response:**

202 	Accepted





### 3. Callback on Subscription Request

This callback API acknowledges the request for subscription from a HIU, and sends back a "id" that will be used when the patient/user approves or denies the subscription.

**URL:** {HIU CALLBACK URL}/v0.5/subscription-requests/hiu/on-init

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
  "timestamp": "2022-06-21T07:48:39.221Z",
  "subscriptionRequest": {
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





### 4. Notification for Subscription Request Grant/Deny/Revoke

This API is used by CM to notify a HIU to grant or deny a request for subscription, and also to notify that in case an existing subscription is revoked or expired. For notifying that a particular subscription request was GRANTED or DENIED, the subscriptionRequestId is passed.

**URL:** {HIU CALLBACK URL}/v0.5/subscription-requests/hiu/notify

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
  "timestamp": "2022-06-21T07:55:50.293Z",
  "notification": {
    "subscriptionRequestId": "request id of the subscription",
    "status": "GRANTED",
    "subscription": {
      "id": "subscription Id",
      "patient": {
        "id": "hinapatel79@sbx"
      },
      "hiu": {
        "id": "HIU_ID"
      },
      "sources": [
        {
          "hip": {
            "id": "HIP_ID"
          },
          "categories": [
            "LINK"
          ],
          "period": {
            "from": "2022-06-21T07:55:50.293Z",
            "to": "2022-06-21T07:55:50.293Z"
          }
        }
      ]
    }
  }
}

```

**Response:**

202 	Accepted





### 5. Callback API for /subscription-requests/hiu/notify to acknowledge receipt of notification.

This API is called by HIU as acknowledgement to subscription request relevant notifications.

**URL:** https://dev.abdm.gov.in/gateway/v0.5/subscription-requests/hiu/on-notify

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
  "timestamp": "2022-06-21T07:59:31.461Z",
  "acknowledgement": {
    "status": "OK",
    "subscriptionRequestId": "subscription Id"
  },
  "error": null,
  "resp": {
    "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  }
}

```

**Response:**

202 	Accepted





### 6. Notification to HIU on basis of a granted subscription

This API is used by CM to notify a HIU for notification relevant to subscription. Notifications are sent to subscribed HIUs whenever a new care-context is linked or new data is available on an existing linked care-context.

if event.category = LINK, then only care-contexts are passed when new care-contexts are linked for patient.
If event.category = DATA, then hiTypes are passed. Care-context is passed only if the subscribed HIU has any valid consent for that care-context

**URL:** {HIU CALLBACK URL}/v0.5/subscriptions/hiu/notify

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
  "timestamp": "2022-06-21T08:01:30.007Z",
  "event": {
    "id": "a1s2c932-2f70-3ds3-a3b5-2sfd46b12a18d",
    "published": "2022-06-21T08:01:30.007Z",
    "subscriptionId": "subscription Id",
    "category": "LINK",
    "content": {
      "patient": {
        "id": "hinapatel79@sbx"
      },
      "hip": {
        "id": "HIP_ID"
      },
      "context": [
        {
          "careContext": {
            "patientReference": "batman@tmh",
            "careContextReference": "Episode1"
          },
          "hiTypes": [
            "OPConsultation"
          ]
        }
      ]
    }
  }
}

```

**Response:**

202 	Accepted




### 7. Callback API for /subscriptions/hiu/notify to acknowledge receipt of notification.

This API is called by HIU as acknowledgement to consent notifications, specifically for cases when consent is REVOKED or EXPIRED.

**URL:** https://dev.abdm.gov.in/gateway/v0.5/subscriptions/hiu/on-notify

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
  "timestamp": "2022-06-21T08:02:56.586Z",
  "acknowledgement": {
    "status": "OK",
    "eventId": "subscription event Id"
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


