---
title: "Link/De-link of ABHA Address"
date: 2022-05-07T18:00:04+05:30
weight: 3
draft: false
---


## Link/De-link of ABHA Address

## Overview of the functionality 

- ABDM has now segregated the identity layer from the consent layer, which will ensure that the ABHA Number (earlier known as Health ID) provides a strong identity to an individual whereas 
an ABHA Address (earlier known as PHR Address) enables an individual to share their health records with different healthcare providers and payers.
- ABHA number can be link/delink with the ABHA address. Below are the API used linking ABHA number with ABHA address.


## Link the ABHA address with ABHA Number

API links the given ABHA Address to the ABHA number and defines whether it is the preferred ABHA Address


### API Sequence 


### API Information Request Response 

Api Checks Health id and Linked it

**URL:** https://healthidsbx.ndhm.gov.in/api/v2/account/phr-linked

**Request:** POST  

**Parameters:**

- Authorization  string (header)

- X-HIP-ID  string (header)

- X-Token  string (header)



**Body:**

phrLinkedOrDeLinkedRequestPayLoad  object (body)

```json
{
  "phrAddress": "string",
  "preferred": true
}
```

**Response:** 200 OK

```json
true
```


## De-Link the ABHA address with ABHA Number


API de-links the given ABHA Address to the ABHA number.


### API Sequence 


### API Information Request Response 

Api Checks Health id and De-linked it

**URL:** https://healthidsbx.ndhm.gov.in/api/v2/account/phr-delinked

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)



**Body:**

phrLinkedOrDeLinkedRequestPayLoad  (body)

```json
{
  "phrAddress": "string"
}
```

**Response:** 200 OK

```json
true
```



## Auto Creation of ABHA address


API used to create the auto creation of ABHA address. X-token has been used in the request body.


### API Sequence 


### API Information Request Response 

Api Accepts HealthID Number and Creates PHR Address

**URL:** https://healthidsbx.ndhm.gov.in/api/v2/account/update/phr-address

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

```json

```

**Response:**

```json
"string"
```

### Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)



