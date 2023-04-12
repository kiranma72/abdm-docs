---
title: "Data request and transfer"
date: 2022-06-22T12:53:25+05:30
weight: 4
draft: false
---



#  Data request and transfer

## Overview of the functionality

The data request and transfer process between the HIU, CM and HIP passes through the following three stages:

### First Stage

- The HIU system initiates data requests for a patient’s health information to the HIP against the relevant consent-artefact, through the CM.

- As part of the data request, the HIU’s health repository embeds three key elements within the health information request:

  - The consent ID corresponding to the consent artefact against which the information request is being made.
  - A data push URL, which is a callback URL that indicates where the information can be pushed by the HIP’s health repository.
    This URL can be different from the HIU’s access URL, provided at the time of registration with the gateway. The HIU can specify a
    different URL for the data flow, in order to keep its identity secret to the extent possible.
  - Several parameters such as the date-time range for the requested and a set of encryption parameters for the HIP repository to encrypt the information.
    The Elliptic-curve Diffie–Hellman based encryption standard is used for encrypting health information.
    
- Upon receipt of the data-request, CM assigns a transaction ID (txn-id) for the entire data flow and communicates this Id to the health repositories of the
HIU and the HIP.

The HIU’s health repository relays all this information to the CM through the gateway.From the CM, the information is relayed to the respective HIP’s health repository (via
the gateway).


### Second Stage

Once the HIP repository receives the information, it first validates the information request, as follows:

 - The HIP finds out if the consent ID corresponds to an expired, paused or revoked artefact.

 - It then checks if the request for which the date-time range corresponds to the range for which the consent artefact allows information access.
   It also ensures that the encryption parameters are correctly defined.
 
 - Once the above checks are made and validated, the HIP health repository encrypts the requested health records and forwards it along with the
   transaction ID to the HIU’s data push URL, after signing the encrypted data with its long-term private key.

### Third Stage

Finally, the CM receives notifications from both the HIP and the HIU. The HIP’s health repository notifies the CM that the requested information 
was transmitted to the HIU. The HIU’s health repository sends a notification that the requested information was
successfully received, or that the request failed.


## API Sequence

All above 3 stages that pertains to HIU are shown in the following diagram:

![Consention of Consent Request](./data_request_and_transfer.PNG)


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



### 2. Health information data request

Request for Health information against a consent id. CM would generate a transactionId against each consent and pass it as trnasaction context / correlation id to the HIP and also return the same to HIU via /on-request.

**URL:** https://dev.ndhm.gov.in/gateway/v0.5/health-information/cm/request

**Request:** POST

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

Access token which was issued after successful login with gateway auth server

- X-CM-ID string (header) :  sbx (or) abdm

Suffix-of-the-consent-manager

**Body:**

```json
{
  "requestId": "a1s2c932-2f70-3ds3-a3b5-2sfd46b12a18d",
  "timestamp": "2022-06-22T09:01:16.382Z",
  "hiRequest": {
    "consent": {
      "id": "string"
    },
    "dateRange": {
      "from": "2022-06-22T09:01:16.382Z",
      "to": "2022-06-22T09:01:16.382Z"
    },
    "dataPushUrl": "string",
    "keyMaterial": {
      "cryptoAlg": "ECDH",
      "curve": "Curve25519",
      "dhPublicKey": {
        "expiry": "2022-06-22T09:01:16.382Z",
        "parameters": "Curve25519/32byte random key",
        "keyValue": "string"
      },
      "nonce": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    }
  }
}

```

**Response:**

202 	Accepted




### 3. Response for Health information data request

Callback API for acknowledgement of Health information request of HIU.
CM calls this API when it has validated the Health Information request given the consent id.
Either the hiRequest or error would need to be specified. If the health info request was valid, then the hiRequest.transactionId specifies the transaction context
against which HIP would send over the data. Possible cases of errors are

- Invalid consent artefact id
- Consent has expired
- Date ranges are invalid

**URL:**  {HIU CALLBACK URL}/v0.5/health-information/cm/on-request

**Request:** POST

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

Access token which was issued after successful login with gateway auth server

- X-HIU-ID string (header) : your-HIU-ID

Identifier of the health information user to which the request was intended

**Body:**

```json
{
  "requestId": "a1s2c932-2f70-3ds3-a3b5-2sfd46b12a18d",
  "timestamp": "2022-06-22T09:04:29.973Z",
  "hiRequest": {
    "transactionId": "a1s2c932-2f70-3ds3-a3b5-2sfd46b12a18d",
    "sessionStatus": "REQUESTED"
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





### 4. Health information transfer API

This API should be implemented at HIU side. It maybe implemented by the Data Bridge representing the HIU.
Entry elements maybe content or link, although for version 1, entry content is preferred.
Entry content (or even link reference content) must be encrypted by means of Elliptic-curve Diffie–Hellman Key Exchange, utilizing the HIU keymaterials that are
passed through the data request API - /v0.5/health-information/hip/request.
Media contains the mimetype of content, and for v1, it is "application/fhir+json"
checksum is Md5 checksum of the data conent, before encryption
Please refer to the ABDM Sandbox documentation for the format of FHIR bundle that is passed through content

**Note:** This API is actually the callback URL that is passed as dataPushUrl in the data request API - /v0.5/health-information/hip/request. This API is directly called by HIP Data Bridge and is not mediated via CM, and hence not routed through the Gateway.

**URL:**  {Data_push_url}/v0.5/health-information/transfer

**Request:** POST

**Parameters:**

- Authorization string (header) : Bearer your-access-token-from-gateway-session

Access token which was issued after successful login with gateway auth server


**Body:**

```json
{
  "pageNumber": 0,
  "pageCount": 0,
  "transactionId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "entries": [
    {
      "content": "Encrypted content of data packaged in FHIR bundle",
      "media": "application/fhir+json",
      "checksum": "string",
      "careContextReference": "RVH1008"
    },
    {
      "link": "https://data-from.net/sa2321afaf12e13",
      "media": "application/fhir+json",
      "checksum": "string",
      "careContextReference": "NCC1701"
    }
  ],
  "keyMaterial": {
    "cryptoAlg": "ECDH",
    "curve": "Curve25519",
    "dhPublicKey": {
      "expiry": "2022-06-22T09:07:16.948Z",
      "parameters": "Curve25519/32byte random key",
      "keyValue": "string"
    },
    "nonce": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
  }
}

```

**Response:**

202 	Accepted



### 5. Notifications corresponding to events during data flow

API called by HIU and HIP during data-transfer.

- HIP on transfer of data would send sessionStatus - one of [TRANSFERRED, FAILED]
- HIP would also send hiStatus for each careContextReference - on of [DELIVERED, ERRORED]
- HIU on receipt of data would send sessionStatus - one of [TRANSFERRED, FAILED]. For example, FAILED when if data was not sent or if invalid data was sent
- HIU would also send hiStatus for each careContextReference - one of [OK, ERRORED]

**URL:**   https://dev.ndhm.gov.in/gateway/v0.5/health-information/notify

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
  "timestamp": "2022-06-22T09:11:03.851Z",
  "notification": {
    "consentId": "a1s2c932-2f70-3ds3-a3b5-2sfd46b12a18d",
    "transactionId": "a1s2c932-2f70-3ds3-a3b5-2sfd46b12a18d",
    "doneAt": "2022-06-22T09:11:03.851Z",
    "notifier": {
      "type": "HIU",
      "id": "tmh"
    },
    "statusNotification": {
      "sessionStatus": "TRANSFERRED",
      "hipId": "max",
      "statusResponses": [
        {
          "careContextReference": "string",
          "hiStatus": "OK",
          "description": "string"
        }
      ]
    }
  }
}

```

**Response:**

202 	Accepted












## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)
