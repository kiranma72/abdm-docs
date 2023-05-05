+++
title = "Managing Consents"
date = 2023-05-02T03:53:25+05:30
weight = 10
chapter = true
pre = "<b>5.10 </b>"
+++

# Managing Consents

## Functionality Overview

- The role of the PHR app is to help the user to manage the consent request.

**The PHR App must:**

1. List all of the consent requests that have been sent to the user

2. Allow the User to edit the content of the consent request and modify it as per their requirements.

3. Allow the user to grant / deny a new consent request.

4. Allow the users to view granted consents and revoke them at any point in time.

## User Experience 

Here's a reference of an ABHA App to help you understand how PHR Applications can do this:

*((add screenshots))*

## Test Cases

**Edit Subscription Request/Disable auto approval request** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit active subscription request|Already granted subscription request can be edited|Check if HI types, types of visit and time period can be edited and saved by clicking on "Save Changes" button"
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Disable auto approval requests|Already granted auto approval policy can be disabled|Check if already granted auto approval policy for health locker can be disabled by clickicking on "Disable" button. Post disble of auto - approval policy|locker request is received from health locker for each record.

## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Managing Consents
PHR App->>HIE-CM: List all consent artefacts <br/> GET /consent-artefacts
PHR App->>HIE-CM: Approve Request <br/> POST/consent-requests/{request-id}/approve
PHR App->>HIE-CM: Deny Request <br/> POST/consent-requests/{request-id}/deny
PHR App->>HIE-CM: Revoke Consents <br/> POST/consents/revoke
{{< /mermaid >}}

## API Collection

