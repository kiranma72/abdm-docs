+++
title = "Store Consent Artefacts"
date = 2023-04-10T12:10:00+05:30
weight = 5
chapter = true
pre = "<b>3.5 </b>"
+++

# Store Consent Artefacts

- All Health Information Providers (HIPs) who are holding any data associated with this consent are notified whenever a consent is granted, revoked, expired or the ABHA address is deleted. 

- THe HIP must save a copy of the consent artefact in their system. Data can be requested against a granted consent any number of times till the **consent expires** (or is revoked by the user).

- When a user revokes a consent - the HIP must ensure that no further data is shared against this consent. 

- If a user deletes their ABHA address, the HIP must remove all references to this ABHA address from their system. This includes all consents related to this ABHA address and also all links between the ABHA address and user profile and health records in their system. Note that HIP/HRPs MUST NOT DELETE the user profile or health data when an ABHA address is deleted. 


## Test Cases

Function|Functionality|Steps To Be Executed 
|--|--|---------|
Grant Consent Request|{{% badge style="blue" %}}Mandatory{{% /badge %}} HIP must save consent (s)granted for a ABHA address in their system (HIP_INIT_GRANT_CONSENT_) | **1.** Initiate a new consent request for HIP on HIU web interface on sandbox. **2.** Grant the request for this consent on PHR app. **3.** HIP will be notified of granted consent request. **4.** Verify the HIP has saved the granted consent request as part of EMR/HMIS system
Revoke Consent Request | {{% badge style="blue" %}}Mandatory{{% /badge %}} HIP must delete consents for  a ABHA address in their system when it is revoked (HIP_INIT_REVOKE_CONSENT) | **1.** Select a granted consent request for this HIP in the PHR app. **2.** Revoke consent on PHR app. **3.** HIP will be notified of revoked consent. **4.** Verify the HIP has deleted the consent as part of EMR/HMIS system upon revoke by patient
Expire Consent Request | {{% badge style="blue" %}}Mandatory{{% /badge %}} HIP must delete consents for  a ABHA address in their system when it is expired (HIP_INIT_EXPIRE_CONSENT) | **1.** Initiate a new consent request for HIP on HIU web interface on sandbox. **2.** Grant the consent on PHR app; Set the expiry to a short expiry time. **3.** HIP will be notified of granted consent request. **4.** HIP will be notified of the expired consent post expiry time. **5.** Verify the HIP has deleted the expired request as part of EMR/HMIS system
ABHA Deactivation | {{% badge style="blue" %}}Mandatory{{% /badge %}} HIP must delete ABHA address  & all associated consents in their system when patient opts out of ABDM (HIP_INIT_ABHA_OPTOUT_DEACTIVATE ) | HIP must delete ABHA address  & all associated consents in their system when patient opts out of ABDM.

## Sample User Experience 

{{< gallery dir="3-milestone2/user-experience" />}} {{< load-photoswipe >}}

{{%icon icon="info-circle" %}} See working with [consents in ABDM Sandbox](/abdm-docs/3-milestone2/understanding-consents/#working-with-consents-in-the-abdm-sandbox)

In order to get a notification ensure that the ABHA address used in the consent request has a care context linked from the HIP you have [registered against your client id](/abdm-docs/1-basics/working_with_abdm_apis/#linking-the-hips--hius-id-for-a-client-id). 

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

**BASE URL:** Callback URL registered by HRP

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/consents/hip/notify$" >}}

**2. Acknowledgement To Notification Of Consents**

**BASE URL:** https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/consents/hip/on-notify$" >}}

