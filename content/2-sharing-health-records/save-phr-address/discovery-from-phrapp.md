---
title: "Discovery from PHR Apps"
date: 2022-05-07T18:00:04+05:30
weight: 4
draft: false
---
## Discovery from PHR Apps : Overview of the functionality 
- Patient must have a PHR app and have a valid PHR address
- Patient LogIn to PHR app with Mobile/PHR Address/e-Mail/ABHA etc
- Patient makes a discovery request with verified identifiers along with name and demographic information 
- HIP revert with the Care Context detail  

 ![alt text](save-phr-address/LoginwithPHR.jpg)

## Discovery of Patient’s information at the HIP

When the gateway calls an HIP system and requests for a particular patient’s records with a set of verifiable Ids, the process of information discovery begins. Upon receipt of the request, the HIP health repository reverts with a set of care context labels (in masked form). The following flow diagram details the flows that take place during patient information discovery from the HIP perspective

## Verify the patient and link the care context as requested by the patient 
This flow begins once a patient initiates a link request to the HIP to link the care context to the patient’s Consent Manager’s User ID. To enable the linking, the HIP system returns a link reference number along with the authentication type and its associated parameters.
The HIP system sends an OTP to the patient’s phone number. Note, the phone number for OTP communication from HIP may be the same as verified by the CM or maybe a different number that the patient has chosen as preferred mode of communication with HIP - meaning it's up to the HIP to choose the phone number it sends OTP to. The patient, via patient app, submits the OTP received from the HIP system within the stipulated time. If the patient is successfully authenticated by the HIP, the linking is now complete. The following flow diagrams details the flows that take place while linking to a health repository representing an HIP
Note : Post successful completion of discovery flow, its HIP’s prerogative to decide regarding implementation logic for saving the Verified identifier information (ABHA Address and ABHA number in case of KYC verified linking
