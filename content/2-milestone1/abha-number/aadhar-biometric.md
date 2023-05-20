+++
title = "Using Aadhar Biometric"
date = 2023-03-16T09:30:25+05:30
weight = 2
chapter = true
pre = "<b>2.1.2 </b>"
+++

# {{%icon icon="bullhorn" %}}Coming Soon.. 
{{% badge style="note" title=" "%}}Note{{% /badge %}} To be documented after V3 APIs are released.

|  Applicable To                             |   HMIS / LMIS (PVT)  |   Government Health App  |  
|-------------------------------|:----------------------:|:--------------------:|
|   Using Aadhar Biometric                      |  {{% badge %}}Optional{{% /badge %}}       |  {{% badge style="blue" %}} Mandatory{{% /badge %}}        | 


{{% notice  title="Overview " icon="list-alt" %}}

- To enable beneficiary registration using Aadhaar Biometric, a client needs to have a [Aadhaar Registered Device (RD Device)](https://uidai.gov.in/images/resource/Aadhaar_Registered_Devices_2_0_4.pdf) that allows capture and processing of Biometrics of the beneficiary.
- This RD Service returns an encrypted PID block containing signed biometrics (using device private key within the registered devices secure zone) back to the calling application.
- To enable beneficiary registration using biometrics, this PID is passed in the request along with Aadhaar and other required details.
- Post verification, the client is returned complete profile data along with ABHA (Health ID).
{{% /notice %}}
