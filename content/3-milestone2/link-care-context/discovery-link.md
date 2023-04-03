+++
title = "Discovery & link"
date = 2023-04-03T04:10:00+05:30
weight = 3
chapter = true
pre = "<b>3.3.3 </b>"
+++

# Discovery & link

## Discovery of the patient’s information at the HIP

- When the gateway calls an HIP system and requests for a particular patient’s records with a set of verifiable Ids, the process of information discovery begins. 

- Upon receipt of the request, the HIP health repository reverts with a set of care context labels (in masked form). 

The following flow diagram details the flows that take place during patient information discovery from the HIP perspective:

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Discovery of patient's information at the HIP
Gateway->>Repository:POST/care-contexts/discover
activate Repository
Repository-->>HIP System:Discovery Request
HIP System-->>Repository:Response
deactivate Repository
Repository->>Gateway:POST/care-contexts/on-discover
{{< /mermaid >}}

## Verify the patient and link the carecontext as requested by the patient

- This flow begins once a patient initiates a link request to the HIP to link the care context to the patient’s Consent Manager’s User ID.

- To enable the linking, the HIP system returns a link reference number along with the authentication type and its associated parameters.

- The HIP system sends an OTP to the patient’s phone number. 
Note, the phone number for OTP communication from HIP may be the same as verified by the CM or maybe a different number that the patient has chosen as preferred mode of communication with HIP - meaning it's up to the HIP to choose the phone number it sends OTP to. 

- The patient, via patient app, submits the OTP received from the HIP system within the stipulated time. If the patient is successfully authenticated by the HIP, the linking is now complete. 

The following flow diagrams details the flows that take place while linking to a health repository representing an HIP:

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Linking (HIP side)
actor User
Gateway->>Repository:POST/v0.5/links/link/init
activate Repository
Repository-->>HIP System:Link init Request
HIP System-->>Repository: Response
Repository->>Gateway:POST/v0.5/links/link/on-init
HIP System-->>User: Send token out-of-band
Gateway->>Repository: POST/v0.5/links/link/confirm
Repository-->>HIP System:Link Confirm Request
HIP System-->>Repository: Response
Repository->>Gateway:POST/v0.5/links/link/on-confirm
deactivate Repository
{{< /mermaid >}}
