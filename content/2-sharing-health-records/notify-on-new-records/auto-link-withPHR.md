
# If the PHR address is available with the HRP, link the care context automatically to the address : #


## Overview of the functionality:
- Patient must have a valid PHR address
- Patient ABHA address is already available with the HIP/HRP.
- Patient already registered in the HRP system
- Demographic auhtentication performed
- Linking token is returned after Demographic authentication
- Using the "linking token" returned above for linking, HIP can subsequently add care-contexts in subsequent API call /links/link/add-contexts


Linking care context automatically is a process where the HIP can link the patient’s care context with the ABHA Address/ABHA Number when the patient already registered in the HIP and his ABHA Address is available with the HRP and has uploaded the health records in their system.

In this patient will have to share their name, YOB, gender which is forwarded to the CM. The CM validates the user details and creates a new access token just for the purpose of linking. This new access token is passed to the HIP. The HIP has to call the CM with the new access token to add the care contexts.



## API Request Response 

1. Get a patient's authentication modes relevant to specified purpose

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/fetch-modes

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-HIP-ID  string (header)

**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T08:51:12.728Z",
  "query": {
    "id": "hinapatel79@ndhm",
    "purpose": "LINK",
    "requester": {
      "type": "HIP",
      "id": "100005"
    }
  }
}
```

**Response:**

202	  Accepted


2. Identification result for a consent-manager user-id

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/on-fetch-modes

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-HIP-ID  string (header)

- X-HIU-ID  string (header)

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T08:53:22.488Z",
  "auth": {
    "purpose": "LINK",
    "modes": [
      "DEMOGRAPHICS"
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

202	 Accepted




3. Initialize authentication from HIP

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/init

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-CM-ID  string (header)

**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T08:59:28.977Z",
  "query": {
    "id": "hinapatel@ndhm",
    "purpose": "LINK",
    "authMode": "DEMOGRAPHICS",
    "requester": {
      "type": "HIP",
      "id": 100005
    }
  }
}
```

**Response:**

202	  Accepted


4. Response to user authentication initialization from HIP

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/on-init

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-HIP-ID  string (header)

- X-HIU-ID  string (header)

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T09:02:38.686Z",
  "auth": {
    "transactionId": "string",
    "mode": "DEMOGRAPHICS",
    "meta": {
      "hint": "string",
      "expiry": "2019-12-30T12:01:55Z"
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




5. Confirmation request sending token, otp or other authentication details from HIP/HIU for confirmation

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/confirm

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-CM-ID  string (header)

**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T09:05:40.735Z",
  "transactionId": "string",
  "credential": {
    "authCode": "string",
    "demographic": {
      "name": "janki das",
      "gender": "M",
      "dateOfBirth": "1972-02-29",
      "identifier": {
        "type": "MOBILE",
        "value": "+919800083232"
      }
    }
  }
}
```

**Response:**

202	  Accepted


6. callback API for /auth/confirm (in case of MEDIATED auth) to confirm user authentication or not

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/on-confirm

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-HIP-ID  string (header)

- X-HIU-ID  string (header)

**Body:**

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-13T09:06:58.238Z",
  "auth": {
    "accessToken": "string",
    "validity": {
      "purpose": "LINK",
      "requester": {
        "type": "HIP",
        "id": 100005
      },
      "expiry": "2022-05-13T09:06:58.238Z",
      "limit": "1"
    },
    "patient": {
      "id": "<patient-id>@<consent-manager-id>",
      "name": "Hina Patel",
      "gender": "M",
      "yearOfBirth": 2000,
      "address": {
        "line": "string",
        "district": "string",
        "state": "string",
        "pincode": "string"
      },
      "identifiers": [
        {
          "type": "MR",
          "value": "+919800083232"
        }
      ]
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

