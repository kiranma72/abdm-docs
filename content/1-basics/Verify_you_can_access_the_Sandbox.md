---
title: "Verify you can access the Sandbox"
date: 2022-05-07T18:00:04+05:30
Weight: 4 
draft: false
pre : "<b>1.4 </b>"
---

## Signing in for the ABDM Sandbox

**Step 1:** Once the Sandbox request form is submitted, the user can see the application submitted status by login in with _Email id_ and _Password_.  
https://sandbox.ndhm.gov.in/applications/Home/login  

![SandboxLogin](/abdm-docs/img/SandboxLogin.png)  

**Step 2:** On login, _Application Submitted_ status (the current application status) is displayed in green.  

![Landing_Page](../Landing_Page.png) 

**Step 3:** Once the application is _Approved_ by the committee, the user will receive an email containing stating _Client id_ & _Client Secret_. On Frontend, the user will see the status changed to _Sandbox Application Status_.  

**Step 4:** Once _Client id_ & _Client Secret_ are received via an email, please verify it and check if the correct response is received. 

###### Create Session

{{< swaggermin src="/abdm-docs/Yaml/ndhm-gateway.yml" api="POST /v0.5/sessions" >}}


**Step 5:** Get certs for JWT Verification


{{< swaggermin src="/abdm-docs/Yaml/ndhm-gateway.yml" api="GET /v0.5/certs" >}}


**Download the Postman Collection** [here](/abdm-docs/Postman/Gateway_Session.json)

**Download the Curls** [here](/abdm-docs/Curls/Gateway_session.txt)
