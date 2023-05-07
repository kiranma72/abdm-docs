+++
title = "Request Health Records"
date = 2023-04-11T05:10:00+05:30
weight = 6
chapter = true
pre = "<b>3.6 </b>"
+++

# Request Health Records

The **data request and transfer** process between the HIU, CM and HIP passes through the following three stages:

**First Stage**

- The HIU system for patient’s health information to the HIP, through the CM against a valid granted consent.
- The CM assigns a transaction ID for the entire data flow and communicates this Id to the health repositories of the HIU and the HIP.
- The HIU’s health repository embeds three key elements within the health information request:
	- The consent ID corresponding to the consent artefact against which the information request is being made.
	- A data push URL, which is a callback URL that indicators where the information can be pushed by the HIP’s health repository. This URL can be different from the HIU’s access URL, provided at the time of registration with the gateway. The HIU can specify a different URL for the data flow, in order to keep its identity secret to the extent possible.
	- Several parameters such as the date-time range for the requested and a set of encryption parameters for the HIP repository to encrypt the information. The Elliptic-curve Diffie–Hellman based encryption standard is used for encrypting health information.

- The HIU’s health repository relays all this information to the CM through the gateway. From the CM, the information is relayed to the HIP’s health repository (via the gateway).

**Second Stage**

Once the HIP repository receives the information, it first validates the information request, as follows:

- The HIP finds out if the consent ID corresponds to an expired, paused or revoked artefact.
- It then checks if the request’s date-time range will correspond to the range for which the consent artefact allows information access. It also ensures that the encryption parameters are correctly defined.
- Once the above checks are made and validated, the HIP health repository encrypts the requested health records and forwards it along with the transaction ID to the HIU’s data push URL, after signing the encrypted data with its long-term private key.

**Third Stage**

Finally, the CM receives notifications from both the HIP and the HIU. The HIP’s health repository notifies the CM that the requested information was transmitted to the HIU. The HIU’s health repository sends a notification that the requested information was successfully received, or that the request failed.

All above 3 stages that pertains to HIP are shown in the following diagram:

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Request for Health Records 
HIE-CM->>HIP/HRP:POST/v0.5/health-information/hip/request
activate HIP/HRP
HIP/HRP-->>HIP/HRP System:notification
HIP/HRP->>HIE-CM:POST/v0.5/health-information/hip/on-request
{{< /mermaid >}}

When HIP gets the request for data transfer, it first **validates the consent:**
1. Consent ID is valid
2. Consent has not expired
3. Data requested is within the consent granted range
4. Only data types that are granted in the consent, are shared

## Sample User Experience 

{{< gallery dir="3-milestone2/data_request_flow" />}} {{< load-photoswipe >}}

## Test Cases

Function|Functionality|Steps To Be Executed 
|--|--|---------|
Data Transfer & Share | {{% badge style="blue" %}}Mandatory{{% /badge %}} HIP must share health records associated with care context on request (HIP_INIT_SHARE_CARECONTEXT)| **1.** Initiate a "Get data" for a linked care context in the PHR app. **2.** HIP will receive a request to share information along with the consent id & end-point URL where the data must be pushed. **3.** HIP must verify that there is a valid consent for sharing this data with the specific HIU making the request. **4.** Health records must be shared only for allowed HIP types withing the date ranges granted in the consent. **5.** HIP should encrypt the health records to be shared with the HIU public key. **6.** HIP should push the encrypted data to the end-point URL. **7.** On successful transfer, HIP must notify HIE-CM of successful transfer by calling health information notify API. **8.** Transfer must be completed within 2 hours of receiving the request.


## API Information Request Response 

**1. Request Health Information**

API called by CM to request Health information from HIP against a validated consent artefact.

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/health-information/hip/request$" >}}

**2. Acknowledge Health Information Request receipt**

API called by HIP to acknowledge Health information request receipt

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/health-information/hip/on-request$" >}}

**3. Data Transfer via Data Push Url**

Health information transfer API.

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/health-information/transfer$" >}}

**Note:** You can send a base64 value of MD5 checksum of the original (pre-encrypted data) so the HIU can verify the integrity of the data once they decrypt it and derive an equivalent checksum and compare it with the value sent as a part of the encrypted data payload.
- you use any online tool like https://emn178.github.io/online-tools/md5_checksum.html to get checksum of the pre-encrypted data.
- convert the obtained checksum value to base64 once you get a checksum value from the previous step.

**4. Data Transfer Notification**

Notifications corresponding to events during data flow

**BASE URL:** https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/health-information/notify$" >}}








