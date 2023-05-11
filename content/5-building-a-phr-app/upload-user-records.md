+++
title = "Uploading User Record"
date = 2023-05-02T03:53:25+05:30
weight = 11
chapter = true
pre = "<b>5.11 </b>"
+++

# Uploading User Record

## Functionality Overview

- PHR Applications must **allow users to scan and upload any records** that they may have with them.
- This includes: physical records, output from IoT devices like BP meter, Glucose meters; and health devices like fit-bit, smartwatches etc
- The PHR application can decide the HI type of the record based on the contents or user input. If the HI type cannot be determined the PHR app is expected to use HI type as “HealthDocumentRecord”.
- The PHR App needs to get a linking token in order to link these health records as a care context to the ABHA address. This is done using the APIs specified in [**Milestone 1.**](/abdm-docs/2-milestone1/verify-abha-address/user-abha-qr-scan/index.html)
- The PHR App must add a care context to the ABHA address of the user for the uploaded records using [**HIP initiated linking.**](/abdm-docs/3-milestone2/link-care-context/hip-initiated-linking/index.html)
- The PHR App needs to ensure the uploaded records can be shared in the ABDM ecosystem. This is achieved by supporting the Health Information Transfer APIs which are specified as part of [**Milestone 2.**](/abdm-docs/3-milestone2/index.html)
