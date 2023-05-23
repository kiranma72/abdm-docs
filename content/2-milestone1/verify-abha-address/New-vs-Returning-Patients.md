+++
title = "New vs Returning Patients"
date = 2023-03-16T09:30:25+05:30
weight = 4
chapter = true
pre = "<b>2.2.4 </b>"
+++

# New vs Returning Patients
|  Applicable To                             |   HMIS / LMIS (PVT)  |   Government Health App  |     
|-------------------------------|:----------------------:|:--------------------:|
|   New vs Returning Patients                      |  {{% badge style="blue" %}} Mandatory{{% /badge %}}       |  {{% badge style="blue" %}} Mandatory{{% /badge %}}        |  

Every Health Facility has to do deal with both new and returning patients. It is important that the capture and saving of a ABHA address be offered to both new and returning patients by the HRP softwares.

## New Patients

For New users, it is recommended that all the demographic information saved by the HRP is exactly the same as in the ABHA Address profile shared by the user. 

## Returning Patients

The following are the recommended steps to be followed by the HRP software:

- Capture the user's ABHA address and profile using any of the above 3 methods.
- Search the HRP system to see if there is an existing patient registration with the same mobile number / name.
- If an existing patient is found - save the ABHA address against existing patients only if the following condition is met:
   - Mobile number is an exact match 
   - Gender is an exact match
   - Age is an exact match or is +/- 2 years 
   - Name is a close phonetic match 

The HRP may also first find a returning patient using a Hosptital MRD Number. In such a case, it is important that the demographic information in the ABHA Address and the information in the HRP is matched to ensure that a incorrect ABHA Address is not linked to any patient. 


## Patients not sharing ABHA Address

It is quite possible that several patients may not share their ABHA address at the time of registration because of reasons like:

- They do not have a ABHA Address or are not aware of ABDM
- They have an ABHA address but decide not to share it with the health facility 

This is prefectly valid and ABDM principles are designed such that the users can decide when to join ABDM and collect their records. 

The HRP software must continue to register patients that do not share their ABHA Address.

