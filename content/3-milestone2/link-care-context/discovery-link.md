+++
title = "Discovery & link"
date = 2023-04-03T04:10:00+05:30
weight = 3
chapter = true
pre = "<b>3.3.3 </b>"
+++


## Discovery and Linking of patient records

- ABDM allows a user to find their health records from any health facility they have visited via the discovery process. 
- Users can use an PHR app to select the health facility they visited and initiate a "Discovery" request 
- The HIE-CM forwards the discovery request to the the HRP linked to the health facility
- All HRPs / HIPs must correctly implement the discovery API
- The HRP is expected to return all the care contexts for the user if records are found 
- The user can then link them to their ABHA address. 

### Sample User Experience

{{< gallery dir="3-milestone2/link-care-context/user-experience" />}} {{< load-photoswipe >}}

### Implementing the discovery algorithm

1. When a discovery request is initiated by the user, the HIP will receive a list of verified identifiers along with name and demographic information. Verified information includes the ABHA address, the mobile number name, gender, year of birth. Unverified / user declared information can include a medical registration number issued by the health facility and shared by the user.

2. The HRP must search for records that match this patient by implementing the matching logic depicted in the flowchart below 

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", sequence":{"showSequenceNumbers":true}}}%%
flowchart LR
id1 -->|Yes| id5((Return<br/>matching Records))
id1{Do any records match ABHA Address?} -->|No| id2{Doany records match Mobile number?}
id2 --> |No| id9{Do any records match <br/>Medical Record Registration number?}
id9 --> |Yes|id3
id9 --> |No|id4((No<br/>matching records<br/>found))
id2 -->|Yes| id3{Does the gender match?}
id3 --> |No| id4
id3 -->|Yes| id6{Is the age within +/- 5 years?}
id6 --> |No| id4
id6 --> |Yes| id7{Is the name phonetically similar?}
id7 --> |No| id4
id7 --> |Yes| id8((Return<br/>matching Records))
{{< /mermaid >}}


3. As response to the discovery request, the HRP/HIP must organize the patient data into [care contexts](/abdm-docs/3-milestone2/understand-care-context/) and respond with a list of care contexts found. Ensure no clinical information is shared in the response. 

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Discovery of patient's information at the HIP
PHR App->>HIE-CM:Discover records at Health Facility
HIE-CM->>HIP/HRP:POST/care-contexts/discover
activate HIP/HRP
HIP/HRP-->>HIE-CM:Response
HIP/HRP->>HIP/HRP:Check if they have any matching records
HIP/HRP->>HIE-CM:POST/care-contexts/on-discover
HIE-CM->>PHR App: List of discovered care contexts
{{< /mermaid >}}

## API Information Request Response 

#### DISCOVERY

**1. Discover patient's accounts**

Request for patient care context discover, made by Gateway intended for a specific HIP.

**BASE URL:** Callback URL registered by HRP

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/care-contexts/discover$" >}}

**2. Response To Patient's Account Discovery Request**

**BASE URL:** https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/care-contexts/on-discover$" >}}

# Linking of discovered care contexts

![Link Record Step 3](/abdm-docs/img/linkrecord-Step3.png)

- This flow begins once a user initiates a link request after discovering care contexts.  
- The User shares the reference number and care contexts to be linked via the PHR app
- On getting the link/init request, the HRP/HIP must send an OTP to the patient’s phone number
- The HIP/HRP then responds with link/on-init to HIE-CM
- The user enters the OTP in the PHR App and the app triggers the link/confirm
- The HIP/HRP verifes the otp and sends the link/on-confirm. 
- On getting the on-confirm, the HIE-CM links the care contexts to the ABHA address 

## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Linking post Discovery (HIP side)
actor User
PHR App->>HIE-CM:Link Care Context
HIE-CM->>HIP/HRP:POST/v0.5/links/link/init
activate HIP/HRP
HIP/HRP-->>User: Send token out-of-band
HIP/HRP->>HIE-CM:POST/v0.5/links/link/on-init
PHR App->>HIE-CM:Confirm link with OTP
HIE-CM->>HIP/HRP: POST/v0.5/links/link/confirm
HIP/HRP->>HIE-CM:POST/v0.5/links/link/on-confirm
{{< /mermaid >}}

#### LINKING

**1. Link Patient's Care Contexts**

**BASE URL:** Callback URL registered by HRP

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/links/link/init$" >}}

**2. Response To Patient's Care Context Link Request**

**BASE URL:** https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/links/link/on-init$" >}}

**3. Token Submission For Link Confirmation**

API to submit the token that was sent by HIP during the link request.

**BASE URL:** Callback URL registered by HRP

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/links/link/confirm$" >}}

**4. Care Context Linkage Completion**

Token authenticated by HIP, confirming linkage of care-contexts

**BASE URL:** https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/links/link/on-confirm$" >}}

