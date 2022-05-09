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

## API Information Request Response 

## Postman + Curl Collection 

