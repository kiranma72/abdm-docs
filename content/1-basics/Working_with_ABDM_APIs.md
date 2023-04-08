---
title: "Working with ABDM APIs"
date: 2022-05-07T18:00:04+05:30
Weight: 7
draft: false
pre : "<b>1.7 </b>"
---

### The Authorization Header

Almost all ABDM APIs require you to pass the session token obtained via your client ID / secret in the Authorization HTTP Header. Remember to add the word "Bearer " in front of the JWT access Token you obtain from the https://dev.abdm.gov.in/gateway/v0.5/sessions

```

Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6IC.....

```


### ABDM Client IDs & Call Back URLs 

- Every organization that registers with ABDM is issued one or more Client IDs 
- Each Client ID should be used by the organization to register ONE INSTANCE of their ABDM compiliant software
- One Client ID can be used to **register** only ONE callback URL.
- Each instance of the software can hold health records for one or more health facilities 
- Each Health Facility is given an ID from the Health Facility Registry. 
- The Facility ID & Client ID need to be **registered** in the ABDM Gateway registry 
- This Facility id must be passed in X-HIP-ID Header in ABDM apis


![Client ID - Callback URL - HIP ID](../clientid-callback.png)


The HIE-CM APIs are designed to be asyncronous. When you call an API on the gateway, if the request is accepted you will merely get a HTTP 200 response acknowledging that the request has been recorded. 

Once the response is available, the gateway will invoke the callback URL registered for the Client ID. All integrators must register a call back URL for their Client ID

The Sequence diagram below provides an example of the asyncronous nature of the ABDM APIs.

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
autonumber
participant client as HRP 
participant gateway as ABDM Gateway
Note over client : Each instance of HRP has a client Id from ABDM
Note over client : Each instance registers a callback Url
client->>gateway: /v0.5/users/auth/fetch-modes
gateway->>client: Response: 200 (as acknowledgment)
Note right of client : asynchronous calls 
gateway->>client: /v0.5/users/auth/on-fetch-modes
client->>gateway: Response: 200 (as acknowledgment)
{{< /mermaid >}}

### Registering your callback URL 
The callback URL is the url for your site where your application recieves APIs calls from the ABDM gateway. After obtaining the client ID and the secret, use the [gateway sessions api](../verify_you_can_access_the_sandbox/#create-session) to get the accessToken. Use the below api, to register the callback  url. Pass the Gateway Session Token in the  ["Authorization:"](#the-authorization-header) header and  the callback url in "url:".  

{{< swaggermin src="/abdm-docs/Yaml/ndhm-devservice.yml" api="PATCH /v1/bridges$" >}}

```
curl --location --request PATCH 'https://dev.abdm.gov.in/devservice/v1/bridges' --header 'Content-Type: application/json' --header 'Authorization: Bearer your-access-token-from-gateway-session' --data-raw '{
	"url": "https://my-emr-site.in"
}
```

{{% badge icon="exclamation-triangle"%}}Disclaimer{{% /badge %}} This API is only available in in sandbox. This is configured via a different API / UI in production

After registering the callback url, if we fire any API which has a callback, ABDM will post the response of the fired API to that callback url.  You can use the [/v1/bridge/getServices](#check-your-configuration) API to check what is configured for your client ID including the callback URL.

### Linking the HIPs / HIUs ID for a Client ID

The HIP code used by ABDM is the same as the [health facility registry ID](https://facility.abdm.gov.in/). 

In the Sandbox you can simply declare a HIP/HIU ID without it being part of the health facility registry. You can use it to link one HIP / HIU ID with your Client ID with no validations.  


{{< swaggermin src="/abdm-docs/Yaml/ndhm-devservice.yml" api="POST /v1/bridges/addUpdateServices$" >}}


All HIUs including PHR apps also need to register a HIU code. 


### Check your configuration 

{{< swaggermin src="/abdm-docs/Yaml/ndhm-devservice.yml" api="GET /v1/bridges/getServices$" >}}


For detailed APIs related to registration with the ABDM gateway 

> https://sandbox.abdm.gov.in/swagger/ndhm-devservice.yaml

### ABDM HTTP Headers

A single ABDM Client (also called a Bridge) can support multiple HIPs / HIUs on the same registered URL. In order to clearly identify which HIP / HIU this message was intented to be sent, the Gateway adds the following headers as part its API calls

1. The X-HIP-ID Header -- Contains the health facility registry code that is linked to the Client ID
2. The X-HIU-ID Header -- Contains the health information user code that is linked to this Client ID

The ABDM architecture is designed to support multiple HIE-CMs. Whenever you call any Gateway API you must include a header that tells the gateway which HIE-CM must this request be sent to 

1. X-CM-ID -- Pass 'sbx' if you are in the sandbox, Pass 'abdm' if you are in production. You must get this from HIE-CM domain name suffixed after the @ symbol in a PHR address. 


### Use Webhook to learn APIs

We recommend using a combination of Postman & webhook to quickly understand ABDM APIs. Use your postman collection and ensure your async callbacks are working in sandbox

1. Go to https://webhook.site 
2. Copy your unique URL (which would be your callback url) shown on the page 
3. [Register it with ABDM Gateway](#registering-your-callback-url). Ensure you get a Response: 200 
4. [Link a HIP / HIU ID of your choice to your client id](#linking-the-hips--hius-id-for-a-client-id). Ensure you get a Response: 200
5. Create a Sandbox ABHA address at [https://phrsbx.abdm.gov.in](https://phrsbx.abdm.gov.in)
4. Call an async Gateway API like /v0.5/users/auth/fetch-modes with the @sbx ABHA address 
5. Verify you get a callback (like /v0.5/users/auth/on-fetch-modes) at your webhook site. It should look like the image below

![webhook-site](/abdm-docs/img/webhook-site-demo.png) 

## Sample User Experience for Callback

{{< gallery dir="1-basics/webhook_callback_flow" />}} {{< load-photoswipe >}}








