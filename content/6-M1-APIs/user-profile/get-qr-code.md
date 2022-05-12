---
title: "Get User QR Code"
date: 2022-05-07T18:00:04+05:30
weight: 2
draft: false
---


## Get User QR Code

## Overview of the functionality 

- Get the User QR code

## API Sequence 


## API Information Request Response 

Get Quick Response code in PNG format for this account

**URL:** https://healthidsbx.ndhm.gov.in/api/v1/account/qrCode

**Request:** GET  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

```json
{
  
}
```

**Response:** 200 OK

```json
{
string
}
```

## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)
