+++
title = "Setup & Manage Subscriptions"
date = 2023-04-25T05:53:25+05:30
weight = 4
chapter = true
pre = "<b>5.4 </b>"
+++

# Setting up & Managing Subscriptions

## Functionality Overview

- In ABDM, any HIU or **PHR Application can subscribe** (that is help you to watch for changes to PHR address) **for notifications** to be received on its callback URL whenever there is a change in the care context linked to a ABHA Address.

- Every PHR App must set up a subscription for the ABHA address:
1. When it creates ABHA address
2. User logs in with a new ABHA address

- PHR applications are expected to provide a UI layer where the user can:
1. View the list of subscriptions
2. Approve subscriptions
3. Deny subscriptions

- The PHR app is responsible for showing up notifications on the Mobile application (for example using Firebase in Android).

- {{% badge %}}Note{{% /badge %}} Users must be explicitly asked to provide a consent to setup the subscription.

- When the user approves the subscription, HIU/PHR App is notified whenever a new care context is linked or updated to the PHR address.

- Once subscribed, the **PHR app will receive notifications in the following events:**
	1. New care context
	2. Modified care context
	3. New consent request
	4. New subscription request

![sample user experienece](/abdm-docs/img/manage-subscriptions.jpg)

## User Experience 

{{< gallery dir="5-building-a-phr-app/subscriptions_apiflow" />}} {{< load-photoswipe >}}

## Test Cases

**Tabs in PHR app (My Records/Linked Facility/Subscriptions)** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Requests" section in the "Subscriptions" tab of PHR app|1) Requested - Not yet any action is taken by individual on consent request received from HIU to PHR app. |All request (consent / subscription / locker) sent by HIU to patiet are seen  in "Requested" dropdown within "Requests" section of PHR app
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Requests" section in the "Subscriptions" tab of PHR app|2) Denied - Individual have "Denied" consent request received from HIU to PHR app. |All denied request (consent / subscription / locker) by patient are seen in "Denied" dropdown within "Requests" section of PHR app. 
3| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Requests" section in the "Subscriptions" tab of PHR app|3) Expired -  Requests is expired because patient have not acted on consent request received in PHR app within the time duration set by HIU|All expired request (consent / subscription / locker) by patient are seen in "Expired" dropdown within "Requests" section of PHR app.
4| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Approved" section in the "Subscriptions" tab of PHR app|1) Granted - Patient had granted the consent request received from HIU to PHR app|All granted request (consent / subscription / locker) by patient are seen in "Granted" dropdown within "Approved" section of PHR app. 
5| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Approved" section in the "Subscriptions" tab of PHR app|2) Revoked - Patient had revoked consent requests after granting it in PHR app. |All revoked request (consent / subscription / locker) by patient are seen in "Revoked" dropdown within "Approved" section of PHR app. 

**Edit Subscription Request/Disable auto approval request** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Edit active subscription request|Already granted subscription request can be edited|Check if HI types, types of visit and time period can be edited and saved by clicking on "Save Changes" button"
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Disable auto approval requests|Already granted auto approval policy can be disabled|Check if already granted auto approval policy for health locker can be disabled by clickicking on "Disable" button. Post disble of auto - approval policy|locker request is received from health locker for each record.


## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Setup Subscriptions
HIU (PHR App)->>HIE-CM:POST /v0.5/subscription-requests/cm/init
HIE-CM-->>HIU (PHR App):POST /v0.5/subscription-requests/hiu/on-init
HIU (PHR App)->>HIE-CM:List Subscription Requests <br/>GET /subscription-requests
HIE-CM-->>HIU (PHR App): Shows the list of Subscriptions Requests
HIU (PHR App)->>HIE-CM: Get subscription details for a subscription ID <br/> GET /subscription-requests/{subscription-id}
HIU (PHR App)->>HIE-CM:Approve Request <br/> POST /subscription-requests/{request-id}/approve
HIU (PHR App)->>HIE-CM:Deny Request <br/> POST /subscription-requests/{request-id}/deny
HIU (PHR App)->>HIE-CM:Notification of request <br/>POST /v0.5/subscription-requests/hiu/notify
HIE-CM-->>HIU (PHR App):POST /v0.5/subscription-requests/hiu/on-notify
{{< /mermaid >}}



## API Information Request Response


#### Setup Subscription 


**1. Request For Subscription**

**BASE URLs:**  https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/subscription-requests/cm/init$" >}}

**2.Callback For Request For Subscription**

**BASE URLs:** https://your-hrp-server.com

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/subscription-requests/hiu/on-init$" >}}

#### User Confirms / Denies The Subscription 

**3. Lists Subscription Requests**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="GET /subscription-requests$" >}}

**4. Get Subscription Details Of A Subscription ID**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="GET ​/subscription-requests​/{subscription-id}$" >}}

**5. Approve Subscription Request**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /subscription-requests/{request-id}/approve$" >}}

**6. Denies Subscription Request**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /subscription-requests/{request-id}/deny$" >}}

#### Notification of subscription to User on PHR app

**7. Notification For Subscription**

**BASE URLs:** https://your-hrp-server.com

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/subscription-requests/hiu/notify$" >}}

**.8 Acknowledge Receipt Of Notification**

**BASE URLs:**  https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/subscription-requests/hiu/on-notify$" >}}


















