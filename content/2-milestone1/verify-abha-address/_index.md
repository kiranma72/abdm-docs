+++
title = "Verification of ABHA Address"
date = 2022-05-07T17:53:25+05:30
weight = 2
chapter = true
pre = "<b>2.2 </b>"
+++

# Verify ABHA Address

**What is ABHA Address?**

ABHA Address is an account on a HIE-CM that enables an user to get this health records linked and share these linked records with consent. 

Users can create an ABHA address via a PHR application, the [NHA HIE-CM Website](https://phr.abdm.gov.in) or by creating a ABHA Number which provides a default ABHA address (14DigitABHANo@abdm). An ABHA address looks like ‘name@abdm’ (production) or 'name@sbx' (Sandbox). 

Users looking to collect their health records digtally are expected to share their ABHA address when they visit a healthcare facility. 

![sharing ABHA addr](/abdm-docs/img/sharing-phr-address-during-reg.png)

This section covers the methods that must be supported for collecting & verifying the ABHA Address from the user:
{{% notice %}}
- Scan Health Facility QR
- Scan User ABHA QR
- By OTP
- New vs Returning Patients
{{% /notice %}}

