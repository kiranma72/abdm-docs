---
title: "Link/De-link of ABHA Address"
date: 2022-05-07T18:00:04+05:30
weight: 3
draft: false
---


## Link/De-link of ABHA Address

## Overview of the functionality 

- ABDM has now segregated the identity layer from the consent layer, which will ensure that the ABHA Number (earlier known as Health ID) provides a strong identity   to an individual whereas an ABHA Address (earlier known as PHR Address) enables an individual to share their health records with different healthcare providers     and payers.
- ABHA number can be link/delink with the ABHA address. Below are the API used linking ABHA number with ABHA address.


## Link the ABHA address with ABHA Number

API links the given ABHA Address to the ABHA number and defines whether it is the preferred ABHA Address


### API Sequence 


### API Information Request Response 

Links the given ABHA Address to the ABHA number

Explanation - API links the given ABHA Address to the ABHA number and defines whether it is the preferred ABHA Address

Request Body - Required

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/phr-linked

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

true


## De-Link the ABHA address with ABHA Number


API de-links the given ABHA Address to the ABHA number.


### API Sequence 


### API Information Request Response 

De-links the given ABHA Address from the ABHA number

Explanation - API delinks a given ABHA Address from the ABHA number

Request Body - Required

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/phr-delinked

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

**Response:** 200  OK

true 



## Auto Creation of ABHA address


API used to create the auto creation of ABHA address. X-token has been used in the request body.


### API Sequence 


### API Information Request Response 

Create ABHA Address With ABHA Number.

Explanation - API Accepts ABHA Number and Creates ABHA Address.

Request Body - Required

Response - API Accepts ABHA Number and Creates ABHA Address. Returns Error for Invalid/Incorrect Info..

**URL:** https://healthidsbx.abdm.gov.in/api/v1/account/update/phr-address

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)



**Response:** 200  OK

1234567890@sbx


### Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Link-De-Link_ABHA_Address_With_ABHA_Number.json)

**Download the Curls** [here](/abdm-docs/Curls/)



