+++
title = "Requesting Consent"
date = 2023-04-17T04:10:00+05:30
weight = 5
chapter = true
pre = "<b>4.1 </b>"
+++

# Requesting Consent

- Whoever wants to ***access health data,*** they have to request for user consent. They do this by sending a consent request with the user's ABHA address to the HIE-CM

- From an **HIU perspective,** the flow begins when the HIU (e.g. a Doctor at a Hospital) requests consent to view patient’s data. 

- Upon **receipt of such a request** from Gateway, CM acknowledges and sends back a consent request ID to the HIU via the gateway.

- The CM then **notifies the patient** that a HIU has made a consent request. The patient can view the request details, and choose to either grant consent or deny it.

- Subsequently, the CM **notifies the HIU requester** of the patient’s consent or denial status via the gateway.

	-	If the request is granted, the CM sends across the Ids of the consent artefacts that were created against the request, to the HIU.
	- If the request is denied, the CM simply notifies the HIU of the denial of the request.

At the time when the patient registers with the hospital (for accessing medical history), this is (can be) initiated when the user scans the Heath facility QR code & registers Health Facility now has user's ABHA address and can initiate a consent request.

## Test Cases

< add >

## API Sequence Diagram

The following diagram explains the consent request creation flow of forwarding the request to the gateway so that gateway can forward it to respective CM:

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Consent Request by HIU
HIU System-->>Repository: Consent Request
activate Repository
Repository->>Gateway: (1) POST/consent-requests/init
Gateway->>Repository: (2) POST/consent-requests/on-init
deactivate Repository
Repository-->>HIU System: Response
Repository->>Gateway: (3) Get Consent Request Status <br/> POST/consent-requests/status
Gateway->>Repository: (4) POST/consent-requests/on-status
{{< /mermaid >}}


## API Information Request Response

**1. Create Consent Request**

Creates a consent request to get data about a patient by HIU user.

**BASE URLs:**  https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/consent-requests/init" >}}


**2. Response To Consent Request**

Result of consent request creation for a patient.

**BASE URLs:**  https://dev.abdm.gov.in/hiu

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/consent-requests/on-init" >}}


**3. Get Consent Request Status**

Get status of consent request done previously

**BASE URLs:**  https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/consent-requests/status" >}}


**4. Callback to Consent Request Status**

Result of consent request done previously. Status of request can be GRANTED, DENIED, EXPIRED

**BASE URLs:**  https://dev.abdm.gov.in/hiu

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hiu.yml" api="POST /v0.5/consent-requests/on-status" >}}
