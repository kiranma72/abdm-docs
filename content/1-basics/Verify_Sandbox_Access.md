---
title: "Verify Sandbox Access"
date: 2022-05-07T18:00:04+05:30
Weight: 4 
draft: false
pre : "<b>1.4 </b>"
---

## Sign in to check application status

**Step 1:** Once the Sandbox request form is submitted, the user can see the application submitted status by login in with _Email id_ and _Password_.  
https://sandbox.ndhm.gov.in/applications/Home/login  

![SandboxLogin](/abdm-docs/img/SandboxLogin.png)  

**Step 2:** On login, _Application Submitted_ status (the current application status) is displayed in green.  

![Landing_Page](../Landing_Page.png) 
{{%icon icon="info-circle" %}} [For additional information on the various application status](../about_abdm_sandbox#abdm-sandbox-journey)

**Step 3:** Once the application is _Approved_ by the committee, the user will receive an email containing your _Client id_ & _Client Secret_. On Frontend, the user will see the status changed to _Sandbox Application Status_.  
![Sandbox_Application_Status](../SandboxApplicationStatus.png) 
{{%icon icon="info-circle" %}} If the status is approved and you havent received the client secret via email, kindly drop a mail{{%icon icon="envelope" %}} to Integration.support@nha.gov.in. Please note that the committee currently meets once a week and it can take 7 - 10 days for you to get your application approved. 

**Step 4:** Once _Client id_ & _Client Secret_ are received via an email, please verify it works by creating a gateway session token. 

###### Create Gateway Session Token 
Server : https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-gateway-v1.yml" api="POST /v0.5/sessions" >}}


###### Verify using Postman 

We recommened you get comfortable using POSTMAN to check various ABDM APIs like the sessions API above.  [Setup Postman ](../postman_setup), download the ABDM API collection and use POSTMAN to verify your client id and secret is able to generate a session token. 


##### Check your JWT token

You can use [jwt.io](https://jwt.io) to see the contents of your gateway session token (accessToken). Paste the accessToken and see what roles have been assigned to your client id. Some ABDM APIs requires your clientID to have specific roles to assigned. You can mail{{%icon icon="envelope" %}} to Integration.support@nha.gov.in to get specific roles added. 

![JWT-IO](../jwt-io.png) 

