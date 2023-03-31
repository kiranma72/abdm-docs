+++
title = "Using Mobile Number"
date = 2023-03-16T09:30:25+05:30
weight = 1
chapter = true
pre = "<b>2.2.1 </b>"
+++

# Using Mobile Number

|  Applicable To                             |   HMIS / LMIS (PVT)  |   Government Health App  |   PHR / LOCKER    |
|-------------------------------|:----------------------:|:--------------------:|:-------------------:|
|   Using Mobile Number                     |  {{% badge %}}Optional{{% /badge %}}       |  {{% badge %}}Optional{{% /badge %}}         |  {{% badge style="blue"%}} Mandatory{{% /badge %}}       |

## API Information Request Response 

**1. Generate OTP**

Api Accepts Mobile Number/Email and then Generates OTP for it.

**BASE URL:** https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/generate/otp$" >}}


**2. Resend OTP**

Api Accepts Transaction Number and then Resend OTP for it.

**BASE URL:** https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/resend/otp$" >}}

**3. Validate OTP**

API to verify the Mobile OTP

**BASE URL:** https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/validate/otp$" >}}

**4. Register the Beneficiary**

Register the Beneficiary to the PHR using the Mobile/Email Address

**BASE URL:** https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app2.yml" api="POST /v1/apps/create/phrAddress$" >}}
