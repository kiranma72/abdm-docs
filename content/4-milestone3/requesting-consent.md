+++
title = "Requesting Consent"
date = 2023-04-17T04:10:00+05:30
weight = 5
chapter = true
pre = "<b>4.1 </b>"
+++

# Requesting Consent


## API Information Request Response

**1. Create Consent Request**

Creates a consent request to get data about a patient by HIU user.

**BASE URLs:**  https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/consent-requests/init" >}}


**2. Response To Consent Request**

Result of consent request creation for a patient.

**BASE URLs:**  https://dev.abdm.gov.in/hiu

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/consent-requests/on-init" >}}


**3. Get Consent Request Status**

Get status of consent request done previously

**BASE URLs:**  https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/consent-requests/status" >}}


**4. Callback to Consent Request Status**

Result of consent request done previously. Status of request can be GRANTED, DENIED, EXPIRED

**BASE URLs:**  https://dev.abdm.gov.in/hiu

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/consent-requests/on-status" >}}
