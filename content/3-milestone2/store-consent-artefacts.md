+++
title = "Store Consent Artefacts"
date = 2023-04-10T12:10:00+05:30
weight = 5
chapter = true
pre = "<b>3.5 </b>"
+++

# Store Consent Artefacts

- Users have the option to **revoke the consent** they have provided to the Health Information User (HIU), at any time. The HIUs must remove any copy of the users' data when the consent is revoked.

- All Health Information Providers (HIPs) who are holding any data associated with this consent are notified. They must save a copy of the consent artefact in their system. Data can be shared against this consent any number of times till the **consent expires** (or is revoked by the user).

- To summarise, if the consent is revoked/expired, they have to get rid of the consent artefacts.

## Test Cases

Function|Functionality|Steps To Be Executed 
|--|--|---------|
Grant Consent Request|{{% badge style="blue" %}}Mandatory{{% /badge %}} HIP must save consent (s)granted for a ABHA address in their system (HIP_INIT_GRANT_CONSENT_) | 1. Initiate a new consent request for HIP on HIU web interface on sandbox. 2. Grant the request for this consent on PHR app. 3. HIP will be notified of granted consent request. 4.Verify the HIP has saved the granted consent request as part of EMR/HMIS system
Revoke Consent Request | {{% badge style="blue" %}}Mandatory{{% /badge %}} HIP must delete consents for  a ABHA address in their system when it is revoked (HIP_INIT_REVOKE_CONSENT) | 1. Select a granted consent request for this HIP in the PHR app. 2. Revoke consent on PHR app. 3. HIP will be notified of revoked consent. 4. Verify the HIP has deleted the consent as part of EMR/HMIS system upon revoke by patient
Expire Consent Request | {{% badge style="blue" %}}Mandatory{{% /badge %}} HIP must delete consents for  a ABHA address in their system when it is expired (HIP_INIT_EXPIRE_CONSENT) | 1. Initiate a new consent request for HIP on HIU web interface on sandbox. 2. Grant the consent on PHR app; Set the expiry to a short expiry time. 3. HIP will be notified of granted consent request. 4. HIP will be notified of the expired consent post expiry time. 5.Verify the HIP has deleted the expired request as part of EMR/HMIS system

## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Notification on Consent Grant
HIE-CM->>HRP/HIP: POST/v0.5/consents/hip/notify
HRP/HIP->>HIE-CM: POST/v0.5/consents/hip/on-notify
{{< /mermaid >}}


## API Information Request Response 

**1. Consent Notification**

**BASE URL:** https://your-hrp-server.com

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/consents/hip/notify$" >}}

**2. Acknowledgement To Notification Of Consents**

**BASE URL:** https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/consents/hip/on-notify$" >}}

## Sample User Experience 

{{< gallery dir="3-milestone2/user-experience" />}} {{< load-photoswipe >}}

{{%icon icon="info-circle" %}} To request HIU (https://dev.ndhm.gov.in/hiu#/hiu/login) login access, kindly drop a mail{{%icon icon="envelope" %}} to integration.support@nha.gov.in.
