---
title: "By scanning HIP QR code"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---

## Overview of the functionality 
- Patient must have a PHR app and have a valid PHR address
- Hospital must generate a HIP QR code and display it at the registration counter
- Patient scans the QR code from his phone camera or his PHR app 
- If scanned from phone camera -- The list of installed PHR apps is shown on the phone. The user can select any of the apps 
- if scanned from within the PHR app, the app will call the share-profile API on the HIE-CM 
- The HIE-CM will verify this is a registered healthcare provider and call the share-profile api on the end of the HRP that is linked to this HIP 
- The HRP software can create a screen to display all the scanned profiles and allow the operator to select them for fast registration 


include any images from the PHR app / EMRSBX for this feature 



## API Sequence 

## Request Response 

## Postman + Curl Collection 

