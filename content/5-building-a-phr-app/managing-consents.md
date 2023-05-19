+++
title = "Managing Consents"
date = 2023-05-02T03:53:25+05:30
weight = 11
chapter = true
pre = "<b>5.11 </b>"
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

![sample user experienece](/abdm-docs/img/manage-consents.gif)

## Test Cases

**Tabs in PHR app (My Records/Linked Facility/Consents)** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Requests" section in the "Consents" tab of PHR app|1) Requested - Not yet any action is taken by individual on consent request received from HIU to PHR app. |All request (consent / subscription / locker) sent by HIU to patiet are seen  in "Requested" dropdown within "Requests" section of PHR app
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Requests" section in the "Consents" tab of PHR app|2) Denied - Individual have "Denied" consent request received from HIU to PHR app. |All denied request (consent / subscription / locker) by patient are seen in "Denied" dropdown within "Requests" section of PHR app. 
3| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Requests" section in the "Consents" tab of PHR app|3) Expired -  Requests is expired because patient have not acted on consent request received in PHR app within the time duration set by HIU|All expired request (consent / subscription / locker) by patient are seen in "Expired" dropdown within "Requests" section of PHR app.
4| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Approved" section in the "Consents" tab of PHR app|1) Granted - Patient had granted the consent request received from HIU to PHR app|All granted request (consent / subscription / locker) by patient are seen in "Granted" dropdown within "Approved" section of PHR app. 
5| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Approved" section in the "Consents" tab of PHR app|2) Revoked - Patient had revoked consent requests after granting it in PHR app. |All revoked request (consent / subscription / locker) by patient are seen in "Revoked" dropdown within "Approved" section of PHR app. 


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

## API Information Request Response

**1. List Consent Artefacts**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="GET /consent-artefacts$" >}}

**2. Approve Requests**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /consent-requests/{request-id}/approve$" >}}

**3. Deny Requests**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /consent-requests/{request-id}/deny$" >}}

**4. Revoke Consents**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /consents/revoke$" >}}





