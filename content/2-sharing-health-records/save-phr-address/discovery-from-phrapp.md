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

<img width="184" alt="LoginwithPHR" src="https://user-images.githubusercontent.com/104073067/169785288-2d900932-7280-4a67-a8db-c84b0fcf462a.jpg">     <img width="184" alt="landingpage" src="https://user-images.githubusercontent.com/104073067/169791285-9e3ff444-2a1f-45a6-82a1-1feaa4f474fb.jpg"> <img width="184" alt="searchHIP" src="https://user-images.githubusercontent.com/104073067/169791298-731f4dcd-9f38-41a3-aff6-2669657699a1.jpg"> <img width="184" alt="linkedHIP" src="https://user-images.githubusercontent.com/104073067/169791288-8930b979-06f5-4245-8118-b64e793f7658.jpg"> <img width="184" alt="fetchrecrd" src="https://user-images.githubusercontent.com/104073067/169791277-da0db504-4efd-466f-839d-352e4f4ffee4.jpg"> <img width="184" alt="foundrecord" src="https://user-images.githubusercontent.com/104073067/169791281-a39409b9-4bee-491c-b7e0-038540119bc1.jpg"> <img width="184" alt="recvrecord" src="https://user-images.githubusercontent.com/104073067/169791295-08455588-73a5-4390-9862-280fef75cbfb.jpg"> <img width="184" alt="linksuccessfully" src="https://user-images.githubusercontent.com/104073067/169791291-a9f19188-2273-4c62-a6ea-f816c10f2dd6.jpg">



## Discovery of Patient’s information at the HIP

When the gateway calls an HIP system and requests for a particular patient’s records with a set of verifiable Ids, the process of information discovery begins. Upon receipt of the request, the HIP health repository reverts with a set of care context labels (in masked form). The following flow diagram details the flows that take place during patient information discovery from the HIP perspective

## Verify the patient and link the care context as requested by the patient 
This flow begins once a patient initiates a link request to the HIP to link the care context to the patient’s Consent Manager’s User ID. To enable the linking, the HIP system returns a link reference number along with the authentication type and its associated parameters.
The HIP system sends an OTP to the patient’s phone number. Note, the phone number for OTP communication from HIP may be the same as verified by the CM or maybe a different number that the patient has chosen as preferred mode of communication with HIP - meaning it's up to the HIP to choose the phone number it sends OTP to. The patient, via patient app, submits the OTP received from the HIP system within the stipulated time. If the patient is successfully authenticated by the HIP, the linking is now complete. The following flow diagrams details the flows that take place while linking to a health repository representing an HIP
Note : Post successful completion of discovery flow, its HIP’s prerogative to decide regarding implementation logic for saving the Verified identifier information (ABHA Address and ABHA number in case of KYC verified linking
