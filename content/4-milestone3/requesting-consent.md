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

**Meta Codes :**

While requesting and exchanging health information, there are meta codes that are relevant to you if you are a HIU.

**Purpose of Use** - defines what is the purpose of use of the health information that a HIU is requesting for. The following are subset from http://terminology.hl7.org/ValueSet/v3-PurposeOfUse


Code|Display
|----|--------|
CAREMGT	| Care Management
BTG	| Break the Glass
PUBHLTH	| Public Health
HPAYMT	| Healthcare Payment
DSRCH	| Disease Specific Healthcare Research
PATRQT	| Self Requested

**Health Information (HI) Types** - defines what types of information a requester is asking for. As of now, the following types are supported.

Code|Display
|----|--------|
Prescription | Prescription
DiagnosticReport | Diagnostic Report
OPConsultation | OP Consultation
DischargeSummary | Discharge Summary
ImmunizationRecord | Immunization Record
HealthDocumentRecord | Record artifact
WellnessRecord | Wellness Record


## Test Cases

S.No|Function|Functionality|Test Case|Steps To Be Executed 
|--|----|------|-----|-----|
1.1|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Patient Discovery HIU_FLOW_101|The System should have a provision to find the patient using ABHA Number or ABHA Address.|1. Enter ABHA Address/ ABHA Number 2. Select Find Patient
1.2|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Consent Request Initiation HIU_FLOW_102"|HIU creates consent request for health records|1. Enter purpose for consent request. 2. Enter duration and expiry of consent request. 3. Enter Health Info type (out of 7 Health Info types). 4. Initiate Request
1.3|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Listing of Consent Requests HIU_FLOW_104|The system should be able to view the list of consent requests inititated|1. List of Consent Requests should include - ABHA| date of creation| date of expiry and Status of request
1.4|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Consent Request is Denied HIU_FLOW_105|The HIU system should not fetch health data for a denied consent request|1. Deny Consent Request on PHR App. 2. Check if data is accessible on the HIU application.
1.5|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Consent Request is Approved HIU_FLOW_106|The HIU system would fetch health data for the approved consent request
1.6|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_107|Fetch health data for (HI Type = DiagnostocReport Structured/Un-Structured)|1. Approve Consent Request on PHR App. 2. Check if data is accessible on the HIU application
1.7|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_108|Fetch health data for (HI Type = Prescription-Structured)|1. Approve Consent Request on PHR App. 2. Check if data is accessible on the HIU application
1.8|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_109|Fetch health data for (HI Type = DischargeSummary-Structured)|1. Approve Consent Request on PHR App. 2. Check if data is accessible on the HIU application
1.9|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_110|Fetch health data for (HI Type = CosultingNote-Structured)|1. Approve Consent Request on PHR App. 2. Check if data is accessible on the HIU application
1.10|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_111|Fetch health data for (HI Type = Immunization record-Structured)|1. Approve Consent Request on PHR App. 2. Check if data is accessible on the HIU application
1.11|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_112|Fetch health data for (HI Type = Health Record-Structured)|1. Approve Consent Request on PHR App 2. Check if data is accessible on the HIU application
1.12|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_113|Fetch health data for (HI Type = Wellness Record-Un-Structured)|1. Approve Consent Request on PHR App. 2. Check if data is accessible on the HIU application

# Sample User Experience

{{< gallery dir="4-milestone3/requestConsentUserExperience" />}} {{< load-photoswipe >}}

- Link a HIU 
- Raise a consent request init using that HIU
- Will receive the response on-init api triggered in the callback url
- User can also check the status of the consent request status(like REQUESTED,GRANTED) by passing the consentid in the consent-requests/status api

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


