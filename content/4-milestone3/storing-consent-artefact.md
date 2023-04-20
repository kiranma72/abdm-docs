+++
title = "Storing Consent Artefacts"
date = 2023-04-17T04:10:00+05:30
weight = 6
chapter = true
pre = "<b>4.2 </b>"
+++

# Storing Consent Artefacts

### Patient Consent notification from CM to HIU

Health Information Users (HIUs) need to be notified on the Users' consent, both when the user grants or revokes consent, or for an expired consent.

A consent can have different forms:

1. **Grant Consent**
- This is when the user grants consent to the HIU to access the health records or health information.

2. **Revoke Consent**
- This is when the user revokes an earlier granted consent from the user, wherein they want to discontinue sharing their health records or heeath information.
- The HIUs have to mandatorily get rid of the health records & information for the users for whose consents have been revoked, to stay ABDM compliant.

3. **Expired Consent**
- This is when a granted consent expires.
- The HIUs have to mandatorily get rid of the health records & information for the users for whose consents expire, to stay ABDM compliant.

The following diagram explains the patient consent notification flow ofrom CM to HIU:

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Consent Notification from CM to HIU
Gateway->>Repository:POST/consents/hiu/notify
activate Repository
Repository-->>HIU System:Notification
note left of Repository: Optional Step: When notifying about <br/> consent being revoked, paused or expired
Repository->>Gateway:POST/consents/hiu/on-notify
deactivate Repository
{{< /mermaid >}}


### Fetching the Consent Artefact

- Once the patient grants consent to the HIU, the CM notifies the HIU system of the consent grant via the gateway. 
- If the patient grants for multiple HIPs, then multiple consent artefacts are generated - one for each HIP. 
- The HIU now first fetches all the consent-artefacts that were generated for his request.

The following diagram shows the flow of how an HIU requests to fetch the consent Artefacts:

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Fetch Consent Artefact
HIU System-->>Repository:Consent-fetch Request
activate Repository
Repository->>Gateway:POST/consents/fetch
Gateway->>Repository:POST/consents/on-fetch
deactivate Repository
Repository-->>HIU System:Response
{{< /mermaid >}}

## Test Cases

S.No|Function|Functionality|Test Case|Steps To Be Executed 
|--|----|------|-----|-----|
1|Revoke Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Revoke Consent HIU_FLOW_202|HIUs should not be able to view health records if the consent is revoked.|**1.** Check list of consent requests to view revoked consents. **2.** Check if health record is visible in case the consent is revoked.
2|Expiry of Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Consent Expiry HIU_FLOW_301|The HIU should not be able to view the health data of an expired consent request|**1.** Provide consent with a short expiry period. **2.** Check status of consent after expiry. **3.** Check if health record is visible to HIU after consent expiry

