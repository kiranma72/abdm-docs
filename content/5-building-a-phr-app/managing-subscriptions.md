+++
title = "Managing Subscriptions"
date = 2023-05-02T03:53:25+05:30
weight = 11
chapter = true
pre = "<b>5.11 </b>"
+++

# Managing Consents and Subscription Requests

## Functionality Overview



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
title Managing Subscriptions
PHR App->>HIE-CM: List all subscription requests <br/> GET/subscription-requests
PHR App->>HIE-CM: Approve Subscription Request <br/> POST/subscription-requests/{request-id}/approve
PHR App->>HIE-CM: Deny Subscription Request <br/> POST/subscription-requests/{request-id}/deny
{{< /mermaid >}}

## API Collection

