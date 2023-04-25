+++
title = "Setup Subscriptions"
date = 2023-04-25T05:53:25+05:30
weight = 3
chapter = true
pre = "<b>5.3 </b>"
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

- The PHR app is responsible for showing up notifications on the Mobile application (for example using Firebase in Android).

![Understanding flow](/abdm-docs/img/setup-subscription.png)


## Test Cases


## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%

{{< /mermaid >}}


## API Information Request Response

