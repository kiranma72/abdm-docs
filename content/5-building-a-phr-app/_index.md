+++
title = "Building a PHR App"
date = 2023-04-24T05:53:25+05:30
weight = 5
chapter = true
pre = "<b>5. </b>"
+++

# Building a PHR Application

Important to understand:
1. All the APIs here are synchronous
2. The interaction is between PHR Application & HIE-CM

The PHR Application has 2 components:
1. PHR App UI
2. PHR App Cloud

Here's a diagram to understand the functionalities of the 2 components:

![setup-subscriptions](/abdm-docs/img/setup-subscriptions.png)

**This section covers:**

{{% notice %}}
1. Create ABHA Address
	- Using Mobile number
	- Using ABHA number
	- Ling / De-link of ABHA address & ABHA number
2. Login & Manage User Profile
3. Setting up subscription
4. Setting up Auto-Approval
5. Handling notifications
6. Discovery & Linking of records
7. Supporting UHI: intent
8. Fetching & Display of Records
9. Managing Consents / Subscription Requests:
	- Listing Consents / Subscription requests
	- Granting Consents / Subscription requests
	- Revoking Consents / Subscription requests
10. Uploading User Record
11. Sharing your PHR address at a Health facility
12. Link/Unlink PHR Address to an ABHA number
{{% /notice %}}
