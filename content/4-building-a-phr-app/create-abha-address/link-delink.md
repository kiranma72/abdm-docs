+++
title = "Link/De-link ABHA Address"
date = 2023-03-30T09:30:25+05:30
weight = 5
chapter = true
pre = "<b>4.2.3 </b>"
+++

# Link and De-Link ABHA Address

## Functionality Overview 

- ABDM has now segregated the identity layer from the consent layer, which will ensure that the ABHA Number (earlier known as Health ID) provides a strong identity   to an individual whereas an ABHA Address (earlier known as PHR Address) enables an individual to share their health records with different healthcare providers and payers.
- ABHA number can be linked or de-linked with the ABHA address. 
- API links the given ABHA Address to the ABHA number and defines whether it is the preferred ABHA Address

## Test Cases

Functionality|Test Case|Steps To Be Executed|
| ----- | ----- | ----- |
{{% badge style="blue" %}}Mandatory{{% /badge %}} Linking of ABHA Number and ABHA Address (LINK_ABHA_701)|System should have provision to link the  created ABHA  number with existing ABHA address |**1.** User will create ABHA  number as deifned in above scenerios. **2.** user should be able to link ABHA  number with existing ABHA address 

## API Sequence Diagram

*check with Kiran*

## API Information Request Response 

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

