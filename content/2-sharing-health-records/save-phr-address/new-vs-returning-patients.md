---
title: "New vs Returning Patients"
date: 2022-05-07T18:00:04+05:30
weight: 4
draft: false
---


Every health facility has to do deal with both new and returning patients. It is important that the capture and saving of a PHR address be offered to both new and returning patients by the HRP software 

## New Patients
For New users, its is recommended that all the demographic information saved by the HRP is exactly the same as in the PHR Address profile shared by the user. 

## Returning Patients

The following is the recommended steps to be followed by the HRP software 

- Capture the users PHR address and profile using any of the above 3 methods
- Search their HRP system to see if there is an existing patient registration with the same mobile number / name
- If an existing patient is found -- save the PHR address against existing patients only if the following condition is met 
   - Mobile number is an exact match 
   - Gender is an exact match
   - Age is an exact match or is +/- 2 years 
   - Name is a close phonetic match 

The HRP may also first find a returning patient using a Hosptital MRD Number. In such a case, it is important that the demographic information in the PHR Address and the information in the HRP are matched to ensure at a incorrect PHR Address is not linked to any patient. 


## Patients not sharing PHR Address

It is quite possible that several patients may not share their PHR address at the time of registration because 

- They do not have a PHR Address or not aware of ABDM
- The have a PHR address but decide not to share it with the health facility 

This is prefectly valid and ABDM principles are designed such that users can decide when to join ABDM and collect their records. 

The HRP software must continue to register patients that do not share their PHR Address.


