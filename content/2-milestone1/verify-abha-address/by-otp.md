+++
title = "By OTP"
date = 2023-03-16T09:30:25+05:30
weight = 3
chapter = true
pre = "<b>2.3.3 </b>"
+++

# By OTP

## API Information Request Response 


**1. Get a patient's authentication modes**

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/fetch-modes

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/users/auth/fetch-modes$" >}}

**2. Accept callback with supported authentication modes for this PHR Address**

**URL:** {HRP CALLBACK URL}/v0.5/users/auth/on-fetch-modes

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/users/auth/on-fetch-modes$" >}}

**3. Initialize authentication from HIP**

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/init

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/users/auth/init$" >}}


**4. Response to user authentication initialization**

**URL:** {HRP CALLBACK URL}/v0.5/users/auth/on-init

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/users/auth/on-init$" >}}

User will get a SMS on their mobile phone with a OTP from the HIE-CM. Collect this OTP from the user and send it via the next API

**5. Confirmation request by sending token, otp**

**URL:** https://dev.abdm.gov.in/gateway/v0.5/users/auth/confirm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/users/auth/confirm$" >}}

Ensure the transaction ID is the same as obtained in the on-init callback

**6. Callback from HIE-CM with KYC and Token information**

**URL:** {HRP CALLBACK URL}/v0.5/users/auth/on-confirm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/users/auth/on-confirm$" >}}


