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
HIU System->>Gateway: 
Gateway->>HIP Repository:POST/health-information/hip/request
activate HIP Repository
HIP Repository-->>HIP System:notification
HIP Repository->>Gateway:POST/health-information/hip/on-request
Note over HIP Repository,HIP System:Prepare data
HIP Repository->>HIU System: 
Note over HIP Repository,HIU System:POST datapush-url<br/>Direct data transfer
HIP Repository->>Gateway:POST/health-information/notify
{{< /mermaid >}}

When HIP gets the request for data transfer, it first **validates the consent:**
1. Consent ID is valid
2. Consent has not expired
3. Data requested is within the consent granted range
4. Only data types that are granted in the consent, are shared


## API Information Request Response 

**1. Request Health Information**

API called by CM to request Health information from HIP against a validated consent artefact.

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/health-information/hip/request$" >}}

**2. Acknowledge Health Information Request receipt**

API called by HIP to acknowledge Health information request receipt

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/health-information/hip/on-request$" >}}

**3. Data Transfer**

Health information transfer API.

**BASE URL:** https://dev.abdm.gov.in/patient-hiu

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST  /v0.5/health-information/transfer$" >}}








