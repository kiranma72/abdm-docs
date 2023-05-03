+++
title = "Handling Notifications"
date = 2023-05-02T03:53:25+05:30
weight = 6
chapter = true
pre = "<b>5.6 </b>"
+++

# Handling Notifications

## Functionality Overview

A PHR Application **handles a variety of notifications for the User.**

Types on notifications to be handled:

1. Care context - new/updated
2. New subscription request (v3 APIs only)
3. New Consent request (v3 APIs only) 
4. Approved / Revoked consents

**Expectation on Care Context - new/updated**

- This happens if a subscription is set up for this ABHA address. whenever there is a new care context linked or updated.
- The PHR App must notify the user on the UI that there is a new health record available.
- If auto-approval policy is in place then the PHR app must make a consent request to fetch a copy of the health record. More information [documented here](/abdm-docs/4-milestone3/requesting-consent/index.html)

**Expectation on New Subscription Request** *(v3 APIs only)*

- Notify the user on the PHR app UI that there’s a new request
- Show the subscription request details
- Allow the user to Approve or Deny the requests

**Expectation on New Consent Request** *(v3 APIs only)*

- Notify the user on the PHR app UI that there’s a new request
- Show the Consent request details
- Allow the user to Grant or Deny the consent

**Expectation on Approved / Revoked Consents**

- Store a copy of consent artefacts
- More information [documented here](/abdm-docs/3-milestone2/store-consent-artefacts/index.html)

If there are user-linked records (that is when it acts as an HRP), then they also need to implement handling consent notifications, as [defined here](/abdm-docs/3-milestone2/store-consent-artefacts/index.html)

## Test Cases

**HIP initiated linking flow**  - When health records are linked with ABHA address at the health facility / health programme

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1|{{% badge style="blue" %}}Mandatory{{% /badge %}}  Post linking of health records with ABHA address by the HIP with patient consent| the individual can view the health records on the PHR mobile app|Health data will be visible in PHR app once HIP link health records with the ABHA address.|Once Individual visits the hospital. • ABHA address is shared with the health programme / health facility. • Individual validates the ABHA address with the mobile OTP. • Post linking of health records with ABHA address by the HIP| the individual can open any PHR app  and click on "Pull Records" button against the visited health programme / health facility| where the record is created and linked to ABHA address to view the record in mobile device.

## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Handling Notifications
PHR App->>HIE-CM: POST /v0.5/subscriptions/hiu/notify
HIE-CM->>PHR App: POST /v0.5/subscriptions/hiu/on-notify
note left of HIE-CM: Acknowledge Receipt Of Notification
{{< /mermaid >}}

## API Information Request Response

#### Change Notification to an ABHA address

Notification to subscribers if care contexts is added / updated.

**8. Notification to HIU**

**BASE URLs:** https://your-hrp-server.com

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/subscriptions/hiu/notify$" >}}

**9. Acknowledge Receipt Of Notification**

**BASE URLs:**  https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/subscriptions/hiu/on-notify$" >}}
