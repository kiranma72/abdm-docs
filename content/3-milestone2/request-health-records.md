+++
title = "Request Health Records"
date = 2023-04-11T05:10:00+05:30
weight = 6
chapter = true
pre = "<b>3.6 </b>"
+++

The **data request and transfer** process between the HIU, HIE-CM and HIP/HRP passes through the following three stages:

**First Stage**

- The HIU system initiates a Health Information request (to the HIE-CM) for an ABHA address for which it has already been granted a consent. 
- The HIE-CM assigns a transaction ID for the entire data flow and communicates this Id to both the HIU and all the HRPs/ HIPs.
- The HIU embeds three key elements within the health information request:
	- The consent ID corresponding to the consent artefact against which the information request is being made.
	- A data push URL, which is the URL where the information must be pushed by the HIP’s health repository. This URL can be different from the HIU’s access URL, provided at the time of registration with the gateway. The HIU can specify a different URL for the data flow, in order to keep its identity secret to the possible extent.
	- Parameters such as the date-time range for the requested and a public key and encryption parameters for the HIP repository to encrypt the information. The Elliptic-curve Diffie–Hellman based encryption standard is used for encrypting the transferred health information.

- The HIU’s health repository relays all this information to the HIE-CM. The HIE-CM triggers the requests to all the HIPs linked to the ABHA address.

**Second Stage**

Once the HIP repository receives the health information request, it performs the following validations:

- The HIP checks the consent ID is available with it and ensures its is not a expired or revoked artefact.
- If the consent id is not available with the HIP a copy can be obtained from the HIE-CM (V3 APIs only)
- The request’s date-time range is cross checked against  the range for which the consent artefact allows information access. 
- Only health records of the HI type allowed in the consent request and for the requested / allowed time period must be selected for transfer
- Once the above checks are made and health records selected, the HIP health repository encrypts the selected health records using the HIU public key.
- The encrypted data is pushed along with with the transaction ID to the HIU’s data push URL.

**Third Stage**

Finally, the HIE-CM receives notifications from both the HIP and the HIU. The HIP’s health repository notifies the HIE-CM that the requested information was transmitted to the HIU. The HIU’s health repository sends a notification that the requested information was successfully received, or that the request failed.

## API Sequence 

All above 3 stages that pertains to HIP are shown in the following diagram:

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Request for Health Records 
HIU->>HIE-CM: Triggers Health Information request 
HIE-CM->>HIP/HRP:POST/v0.5/health-information/hip/request
activate HIP/HRP
HIP/HRP->>HIE-CM:POST/v0.5/health-information/hip/on-request
HIP/HRP->>HIP/HRP: Select Health records, encrypt data
HIP/HRP-->>HIU: POST {HIUdatapushURL}/v0.5/health-information/transfer
HIP/HRP->>HIE-CM: POST /v0.5/health-information/notify
HIU->>HIE-CM: Notify transfer recieved
{{< /mermaid >}}


## Sample User Experience 

![data_request_flow](../data_request.gif)

See [Working with consents in the ABDM sandbox](/abdm-docs/3-milestone2/understanding-consents/#working-with-consents-in-the-abdm-sandbox) to trigger a Health Information request to your HIP/HRP. 

Remember to use an ABHA address that has a care context linked to your HIP/HRP for this experience.

## Test Cases

Function|Functionality|Steps To Be Executed 
|--|--|---------|
Data Transfer & Share | {{% badge style="blue" %}}Mandatory{{% /badge %}} HIP must share health records associated with care context on request (HIP_INIT_SHARE_CARECONTEXT)| **1.** Initiate a "Get data" for a linked care context in the PHR app. **2.** HIP will receive a request to share information along with the consent id & end-point URL where the data must be pushed. **3.** HIP must verify that there is a valid consent for sharing this data with the specific HIU making the request. **4.** Health records must be shared only for allowed HIP types withing the date ranges granted in the consent. **5.** HIP should encrypt the health records to be shared with the HIU public key. **6.** HIP should push the encrypted data to the end-point URL. **7.** On successful transfer, HIP must notify HIE-CM of successful transfer by calling health information notify API. **8.** Transfer must be completed within 2 hours of receiving the request.


## API Information Request Response 

**1. Request Health Information**

API called by HIE-CM to request health information from HIP against a validated consent artefact.

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/health-information/hip/request$" >}}

**Note:** Fidelius is designed to automatically handle both formats of public keys (base64 encoded, uncompressed public key format & x509PublicKey format) but the recommended format for sending the public key is *"base64 encoded, uncompressed public key format”*.
![public key formats](../public_key_formats.png)
**2. Acknowledge Health Information Request receipt**

API called by HIP to acknowledge health information request receipt

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/health-information/hip/on-request$" >}}

**3. Data Transfer via Data Push Url**

Health information transfer API.

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/health-information/transfer$" >}}

**Note:** You can send a base64 value of MD5 checksum of the original (pre-encrypted data) so the HIU can verify the integrity of the data once they decrypt it and derive an equivalent checksum and compare it with the value sent as a part of the encrypted data payload.
- Try using the tool like https://emn178.github.io/online-tools/md5_checksum.html to get checksum of the pre-encrypted data when working with postman
- convert the obtained checksum value to base64 once you get a checksum value from the previous step.

**4. Data Transfer Notification**

Notifications corresponding to events during data flow

**BASE URL:** https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/health-information/notify$" >}}








