---
title: "By scanning PHR Address QR"
date: 2022-05-07T18:00:04+05:30
weight: 2
draft: false
---

## Overview of the functionality 
- Patient must have a PHR app or PHR card and have a valid PHR address
- Hospital must have a scanner available at the registration counter
- Hospital operator scans the QR code on patient PHR card or from PHR mobile App.
- If scanned from within the PHR app, the app will call the share-profile API on the HIE-CM 
- The HIE-CM will verify this is a registered healthcare provider and call the share-profile api on the end of the HRP that is linked to this HIP 
- The HRP software can create a screen to display all the scanned profiles and allow the operator to select them for fast registration 
- Then the detials like ABHA ID, PHR address,name,gender,sateId,districtId,dob,address will be shared with health facility


include any images from the PHR app / EMRSBX for this feature 



## API Sequence 

1. Get patient's authentication modes relevant to specified purpose (KYC & link is used most frequently)

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/fetch-modes
**Request:** POST  
**Parameters:**
- Authorization: Access token which was issued after successful login with gateway auth server.
Authorization
Type: string (header)

- X-CM-ID: Suffix of the consent manager to which the request was intended.
X-CM-ID 
Type: string (header)

**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-10T04:36:30.435Z",
  "query": {
    "id": "hinapatel79@ndhm",
    "purpose": "LINK",
    "requester": {
      "type": "HIP",
      "id": "100005"
    }
  }
```
**Response:**
202	
Request Accepted



2. Initialize Authentication from HIP
Demographic auth mode to be used for QR code scans. Direct auth modes to be used for verbal sharing.


**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/init
**Request:** POST  
**Parameters:**
- Authorization: Access token which was issued after successful login with gateway auth server.
Authorization
Type: string (header)

- X-CM-ID: Suffix of the consent manager to which the request was intended.
X-CM-ID 
Type: string (header)

**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-10T08:17:50.254Z",
  "query": {
    "id": "hinapatel@ndhm",
    "purpose": "LINK",
    "authMode": "MOBILE_OTP",
    "requester": {
      "type": "HIP",
      "id": 100005
    }
  }
```
**Response:**
202	
Request Accepted



3. Confirm authentication of users. Obtain linking token

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/confirm
**Request:** POST  
**Parameters:**
- Authorization: Access token which was issued after successful login with gateway auth server.
Authorization
Type: string (header)

- X-CM-ID: Suffix of the consent manager to which the request was intended.
X-CM-ID 
Type: string (header)

**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-10T08:20:25.720Z",
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
```
**Response:**
202	
Request Accepted



4. Notification API in case of DIRECT mode of authentication

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/on-notify
**Request:** POST  
**Parameters:**
- Authorization: Access token which was issued after successful login with gateway auth server.
Authorization
Type: string (header)

- X-CM-ID: Suffix of the consent manager to which the request was intended.
X-CM-ID 
Type: string (header)

**Body:**
```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "2022-05-10T08:21:51.727Z",
  "acknowledgement": {
    "status": "OK"
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
202	
Request Accepted


## API Information Request Response 

## Postman + Curl Collection 

