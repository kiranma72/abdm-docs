+++
title = "Setup Subscriptions"
date = 2023-04-25T05:53:25+05:30
weight = 4
chapter = true
pre = "<b>5.4 </b>"
+++

# Setting up Subscriptions

## Functionality Overview

- In ABDM, any HIU or **PHR Application can subscribe** (that is help you to watch for changes to PHR address) **for notifications** to be received on its callback URL whenever there is a change in the care context linked to a ABHA Address.

- Every PHR App must set up a subscription for the ABHA address:
1. When it creates ABHA address
2. User logs in with a new ABHA address

- {{% badge %}}Note{{% /badge %}} Users must be explicitly asked to provide a consent to setup the subscription.

- Once subscribed, the **PHR app will receive notifications in the following events:**
	1. New care context
	2. Modified care context
	3. New consent request
	4. New subscription request

![setup-subscriptions](/abdm-docs/img/setup-subscriptions.png)

- The PHR app is responsible for showing up notifications on the Mobile application (for example using Firebase in Android).

![Understanding flow](/abdm-docs/img/setup-subscription.png)


## User Experience 

{{< gallery dir="5-building-a-phr-app/subscriptions_apiflow" />}} {{< load-photoswipe >}}

## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Set-up Subscriptions
PHR App->>HIE-CM:add
HIE-CM->>PHR App:add
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

**4. Approve Subscription Request**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /subscription-requests/{request-id}/approve$" >}}

**5. Denies Subscription Request**

**BASE URLs:**  https://dev.abdm.gov.in/cm

{{< swaggermin src="/abdm-docs/Yaml/ndhm-phr-app.yml" api="POST /subscription-requests/{request-id}/deny$" >}}

#### Notification of subscription to User on PHR app

**6. Notification For Subscription**

**BASE URLs:** https://your-hrp-server.com

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/subscription-requests/hiu/notify$" >}}

**7. Acknowledge Receipt Of Notification**

**BASE URLs:**  https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/subscription-requests/hiu/on-notify$" >}}








