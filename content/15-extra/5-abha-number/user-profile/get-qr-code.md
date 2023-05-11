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

Get Quick Response code in PNG format for this account.

Explanation - Api Accepts Auth Token and then returns Account Info for QR Code.

Request Body - Required

Responce - Api Accepts Auth Token and then returns Account Info for QR Code. Returns Error for Unauthorized Token.

**URL:** https://healthidsbx.abdm.gov.in/api/v1/account/qrCode

**Request:** GET  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)



**Response:** 200 OK

string


## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/Get_User_QRCode.json)

**Download the Curls** [here](/abdm-docs/Curls/)
