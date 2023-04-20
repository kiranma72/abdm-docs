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
  "requestId": "da98c401-a188-48c0-b97d-bba04c7c2c12",
  "timestamp": "2022-07-08T11:16:43.665Z",
  "subscription": {
    "purpose": {
      "text": "Care Management",
      "code": "CAREMGT",
      "refUri": "string"
    },
    "patient": {
      "id": "hinapatel79@sbx"
    },
    "hiu": {
      "id": "HIU-ID"
    },
    "hips": [
      {
        "id": "HIP-ID"
      }
    ],
    "categories": [
      "LINK"
    ],
    "period": {
      "from": "2022-06-16T08:54:51.397Z",
      "to": "2022-07-25T08:54:51.397Z"
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
  "requestId": "e7cb5bcf-b1f1-477d-bf04-637217009708",
  "timestamp": "2022-07-08T11:14:19.12645",
  "subscriptionRequest": {
    "id": "a38aa587-70c6-4b3e-9d76-93fc7e9fd410"
  },
  "error": null,
  "resp": {
    "requestId": "983c4a30-271c-4add-b50f-85c88b6ded8f"
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
  "requestId": "5f680014-cd8e-4cf8-8a3a-79f1ce3e7c23",
  "timestamp": "2022-07-08T11:18:21.418348",
  "notification": {
    "subscriptionRequestId": "a38aa587-70c6-4b3e-9d76-93fc7e9fd410",
    "status": "GRANTED",
    "subscription": {
      "id": "42d4f25f-b8f4-4c52-80a5-11b02de1ad2f",
      "patient": {
        "id": "hinapatel79@sbx"
      },
      "hiu": {
        "id": "HIU-ID",
        "name": "HIU NAME"
      },
      "sources": [
        {
          "hip": {
            "id": "HIP-ID",
            "name": "HIP NAME"
          },
          "categories": [
            "LINK"
          ],
          "period": {
            "from": "2022-06-16T08:54:51.397",
            "to": "2022-07-25T08:54:51.397"
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
  "requestId": "e2b422c4-8026-4931-bfa3-111c2accd1c7",
  "timestamp": "2022-07-08T11:32:28.779000",
    "acknowledgement": {
        "status": "OK",
        "subscriptionRequestId": "a38aa587-70c6-4b3e-9d76-93fc7e9fd410"
    },
    "error": null,
    "resp": {
        "requestId": "5f680014-cd8e-4cf8-8a3a-79f1ce3e7c23"
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
  "requestId": "07cc2f96-ff63-4f49-b11a-354599a7f299",
  "timestamp": "2022-07-08T11:27:43.230328",
  "event": {
    "id": "add38a15-1bf3-4132-bca9-24ddc1830238",
    "published": "2022-07-08T11:27:43.190529",
    "subscriptionId": "42d4f25f-b8f4-4c52-80a5-11b02de1ad2f",
    "category": "LINK",
    "content": {
      "patient": {
        "id": "hinapatel79@sbx"
      },
      "hip": {
        "id": "HIP-ID",
        "name": "HIP NAME"
      },
      "context": [
        {
          "careContext": {
            "patientReference": "hinapatel79@sbx",
            "careContextReference": "01012021123"
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
  "requestId": "b185f11e-3277-4d47-8a2c-16b86daccc73",
  "timestamp": "2022-07-08T11:32:28.779000",
    "acknowledgement": {
        "status": "OK",
        "eventId": "add38a15-1bf3-4132-bca9-24ddc1830238"
    },
    "error": null,
    "resp": {
        "requestId": "07cc2f96-ff63-4f49-b11a-354599a7f299"
    }
}

```

**Response:**

202 	Accepted




## Postman + Curl Collection 

**Download the Postman Collection** [here](./Subscription_Flow.json)

**Download the Curls** [here](/abdm-docs/Curls/)


