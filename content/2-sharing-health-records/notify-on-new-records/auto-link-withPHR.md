
---
title: "Link a new record"
date: 2022-05-07T18:00:04+05:30
weight: 2
draft: false
---

### Overview of the functionality:
- Patient must have a valid PHR address
- Patient PHR address is already shared with HIP/HRP either during registration or discovery method
- A new health record is generated for this patient at the HRP
- The HRP checks if it has a valid linking token saved or obtains a new token via demographic auth
- The HRP decides if it will create a new care context for this health record or add to an existing care context
- If it is a new care context then the HRP links it with the PHR address
- If it is an existing care context, The HRP updates the existing care context  


Following is the API sequence diagram :

![Deep Linking](../link-records.jpg)



### API Request Response 

#### 1. Add the care context to the PHR address 

**URL:**
**https://dev.abdm.gov.in/gateway/v0.5/links/link/add-contexts**

**METHOD**: POST

**HEADERS**:
- Authorization: Session Token using Client ID
- X-CM-ID: sbx or adbm. Must be the same as the domain in the PHR address

**Request Body:**
```
{
     "requestId": "{{$guid}}",
     "timestamp": "{{timestamp}}",
    "link": {
        "accessToken": "eyJhbGciOiJSUzUxMiJ9.eyJzdWIiOiJraXJhbm1hQHNieCIsInJlcXVlc3RlclR5cGUiOiJISVAiLCJyZXF1ZXN0ZXJJZCI6IktULUhJUCIsInBhdGllbnRJZCI6ImtpcmFubWFAc2J4Iiwic2Vzc2lvbklkIjoiMzM4OWUwZGEtNzUyNS00OGNlLWIwYTMtZTdlMzk5ZjY0N2ZlIiwiZXhwIjoxNjU0NjU5MjYxLCJpYXQiOjE2NTQ1NzI4NjF9.ZNn9cmMiEWmiXm1X014RL7kls0dZ8knZe9COA8jrDAlNroyofi_DEjydDiwTMiaI0wIxvz8cOxth2trLiGdOri7LWpHSYqe4OPI_w7_KFFdOtRVZg_guAnX4NvEIicoU4fScHEEJRlzmiSskzUXSjbHqf1dz9qcKOH5-Mv9hA8zglBdxqH0X4OFBaDlyOgSSh2o5QEUvbM1hV1gl9ll1InnYgTTvBHlqg-KOYKK9lS6SVHDsKq3ULeguHFGCCNaBvLWr6-C6Hlf7oiqJsV-DoSISbezUPNa4vdMrwgAnCEaCsQFC-H-On5AbFpf7IM472gFVAj9s3tspaW1fC--bCw",
        "patient": {
            "referenceNumber": "demo-care-context-21",
            "display": "OPD Records on 02-Jun-2022",
            "careContexts": [
                {
                    "referenceNumber": "demo-care-context-21",
                    "display": "OPD Records on 02-Jun-2022"
                }
            ]
        }
    }
}
```

**Response**
202 Accepted 

#### 2. Ensure response is a success 

**URL:** 
**{HRP CALLBACK URL}/v0.5/links/link/on-add-contexts**

**METHOD**: POST

**HEADERS**:
- Authorization: Gateway JWT Token
- X-HIP-ID: The HIP ID with which the access token was generated


**Request Body:**
```
{
  "requestId": "53e6d0dc-aecb-4027-a526-a13bd803f6f5",
  "timestamp": "2022-06-07T03:34:56.173438",
  "acknowledgement": {
    "status": "SUCCESS"
  },
  "error": null,
  "resp": {
    "requestId": "2b08d89e-fc37-47d3-bf02-946bbf85c583"
  }
}
```

**Error if same care context is shared for linking**

```
{
  "requestId": "5368150b-60cb-4d23-8c61-cd35b6c3f633",
  "timestamp": "2022-06-07T03:53:35.825703",
  "acknowledgement": null,
  "error": {
    "code": 1439,
    "message": "Some of the Care Contexts are already linked, please remove the linked Care Contexts."
  },
  "resp": {
    "requestId": "727ebb6e-9285-4f14-8c61-4e45e7a011d6"
  }
}
```