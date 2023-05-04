+++
title = "Setup Auto-Approval"
date = 2023-05-02T03:53:25+05:30
weight = 5
chapter = true
pre = "<b>5.5 </b>"
+++

# Setting up Auto-Approval

## Functionality Overview

- The PHR App should get confirmation from the user that it can automatically retrieve any new linked health records and save a copy in the PHR application.
- On confirmation from the user, the PHR app can set up an auto-approval policy with the HIE-CM.
- The HIE-CM responds with an auto-approval ID that must be saved by the PHR app.
- When the PHR App receives a notification for a new care context or update of a care context, it is expected to initiate a consent request to the HIE-CM for access to the linked care context
- Since the auto approval policy is in place the HIE-CM will immediately respond with a consent grant to the PHR app.
- The PHR App can now use the approved consent to retrieve a copy of the health record and save it.

## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Setup Auto-Approval
PHR App->>HIE-CM: Setup auto-approval for HIU<br/>POST/consents/auto-approve
note over HIE-CM,PHR App:Returns Auto-Approval Id
PHR App->>HIE-CM: Enable auto-approval-policy<br/>POST/consents/auto-approval-policy/{auto-approval-id}/enable
PHR App->>HIE-CM: Disable auto-approval-policy<br/>POST/consents/auto-approval-policy/{auto-approval-id}/disable 
{{< /mermaid >}}



## API Information Request Response


#### Auto Approval

**1. Notification to HIU**

**BASE URLs:** https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /consents/auto-approve$" >}}

#### Enable/Disable Auto-Approval 

**2. Disable Auto-Approval Policy**

**BASE URLs:** https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /consents/auto-approval-policy/{auto-approval-id}/disable$" >}}

**3. Enable Auto-Approval Policy**

**BASE URLs:** https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /consents/auto-approval-policy/{auto-approval-id}/enable$" >}}

