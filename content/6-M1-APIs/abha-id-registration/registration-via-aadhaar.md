---
title: "ABHA ID Registration via Aadhaar"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---


## Registration via Aadhaar Number



To enable beneficiary registration using Aadhaar OTP, an integrator needs to generate an Aadhaar OTP, followed by OTP verification. Once the OTP is verified, the client is returned complete profile data along with ABHA (Health ID) Number. 

To enable beneficiary registration using Aadhaar Biometric, a client needs to have a Aadhaar Registered Device (RD Device) that allows capture and processing of Biometrics of the beneficiary This RD Service returns an encrypted PID block containing signed biometrics (using device private key within the registered devices secure zone) back to the calling application.  
To enable beneficiary registration using biometrics, this PID is passed in the request along with Aadhaar and other required details. Post verification, the client is returned complete profile data along with ABHA (Health ID).  

Note: Mobile Number can be linked/verify with ABHA via using API  







