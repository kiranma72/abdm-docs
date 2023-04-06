+++
title = "HIP Initiated linking"
date = 2023-04-03T04:10:00+05:30
weight = 1
chapter = true
pre = "<b>3.3.1 </b>"
+++

# HIP Initiated linking

**Applicable when:** User has come to the hospital & abha address has been captured during registration

- When a new health record is created for the patient, it needs to be linked to the ABHA address (HIP initiated linking)

- If linking token has expired, a new link token is obtained via demo auth & health record must be linked.

Here's more to understand on **HIP initiated linking:**

- Whenever a new health record is created for a patient, decide which care context this will be a part of.

- The HRP must link the care context as soon as the health record is ready to be shared with the user

- We link the care context using the linking token with the ABHA address.

- When the user has shared their ABHA address; if the user does not have a valid token, then they need to generate linking token, that is when they do [demographic auth.](/abdm-docs/2-milestone1/abha-number/aadhar-demographic/index.html)

- Whenever a **new care context is linked** or an **existing care context is updated** with new health records, a notification is sent to all PHR applications that have subscribed to receive notifications for this ABHA address.

## Test Cases

**Function:** Health Record Creation

Functionality|Test Case|Steps To Be Executed 
|------|-----|-----|
{{% badge style="blue" %}}Mandatory{{% /badge %}} Creation of Health Records (Health_RECORD_CREATION_101)|The system should have a provision to create digital health records|1. Check if digital Health Records are being created in HIP systems (valid for HI types as applicable to the integrating entity). 2.Recommend to have the health record in FHIR format.

**Function:** HIP Initiated Health Record Linking Using Mobile OTP

Functionality|Test Case|Steps To Be Executed 
|------|-----|-----|
{{% badge style="blue" %}}Mandatory{{% /badge %}} Link record via mobile OTP (HIP_INTI_LINK_201)|The system should have provision to link patient's Health record with ABHA address |1. Enter patient's ABHA address on the System. 2. OTP receive by the patient.
{{% badge style="blue" %}}Mandatory{{% /badge %}} OTP validation (HIP_INTI_LINK_203)|The user shares the OTP with the HIP for validation|1. Share Mobile OTP with HIP System. 2. Validate the OTP. 3. Upon successful validation of OTP| linking token is generated.
{{% badge style="blue" %}}Mandatory{{% /badge %}} Linking of Health Records (HIP_INTI_LINK_205)|HIP system links the ABHA Number / Address with the patient records|1. Link Health Records. 2. Through PHR Application| check if the linked records can be pulled

**Function:** HIP Initiated Health Record Linking Using Aadhaar OTP

Functionality|Test Case|Steps To Be Executed 
|------|-----|-----|
{{% badge style="blue" %}}Mandatory{{% /badge %}} Link record via aadhaar linked mobile  OTP (HIP_INTI_LINK_301)|The system should have provision to link patient's Health record with ABHA address |1. Enter patient's ABHA address on the System. 2. OTP receive by the patient.
{{% badge style="blue" %}}Mandatory{{% /badge %}} OTP validation (HIP_INTI_LINK_303)|The user shares the OTP with the HIP for validation|1. Share Mobile OTP with HIP System. 2. Validate the OTP. 3. Upon successful validation of OTP| linking token is generated."
{{% badge style="blue" %}}Mandatory{{% /badge %}} Linking of Health Records (HIP_INTI_LINK_305)|HIP system links the ABHA Number / Address with the patient records|1. Link Health Records. 2. Through PHR Application| check if the linked records can be pulled

**Function:** HIP Initiated Health Record Linking Using Direct Auth

Functionality|Test Case|Steps To Be Executed 
|------|-----|-----|
{{% badge style="blue" %}}Mandatory for the Govt. Integartors{{% /badge %}} Direct Auth mode for Linking of Health Records (HIP_INTI_LINK_401)|The system should have provision to link patient's Health record with ABHA address |1. Enter patient's ABHA address on the System. 2. The user logs into their PHR Application| receives the request for approval and approves it. 3. Search the request in the Notification tab. 4. Approve the request.(User may approve or reject the request. if the request is rejected process ends there). 5. Upon successful validation of OTP| linking token is generated.
{{% badge style="blue" %}}Mandatory{{% /badge %}} Linking of Health Records (HIP_INTI_LINK_404)|HIP system links the ABHA Address with the patient records|1. Link Health Records. 2. Through PHR Application| check if the linked records can be pulled.

**Function:** HIP Initiated Health Record Linking Using Demographic Auth

Functionality|Test Case|Steps To Be Executed 
|------|-----|-----|
{{% badge style="blue" %}}Mandatory for the Govt. Integartors  {{% /badge %}} Link record via Demographic Auth (HIP_INTI_LINK_501)|The system should have provision to link patient's Health record with ABHA address.|1. for the verified ABHA Address of the patient in the HIP System. 2.The user provides their demographic details (name, gender, DOB, mobile number). 3. Enter user/patient's demographic details in the HIP System
{{% badge style="blue" %}}Mandatory{{% /badge %}} Validate the demographic details  (HIP_INTI_LINK_503)|The HIP validates demographic details of patient|1. Validate Demographic Details ( Provided by the user and fetch by the ABHA address). 2.Upon successful validation of OTP| linking token is generated.
{{% badge style="blue" %}}Mandatory{{% /badge %}} Linking of Health Records (HIP_INTI_LINK_505)|HIP system links the ABHA Address with the patient records|1. Link Health Records. 2. Through PHR Application| check if the linked records can be pulled"

## API Sequence Diagram

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title HIP Initiated Linking
activate HRP/HIP
activate ABDM Gateway
HRP/HIP->>ABDM Gateway: POST/hiecm/api/v3/link/carecontext
ABDM Gateway-->>HRP/HIP: return
deactivate HRP/HIP 
deactivate ABDM Gateway
activate HRP/HIP  
activate ABDM Gateway  
ABDM Gateway->>HRP/HIP:(callback_url)/v3/hip/link/on-carecontext
HRP/HIP-->>ABDM Gateway:return
deactivate HRP/HIP 
deactivate ABDM Gateway
ABDM Gateway->>PHR App:(callback_url)/v3/hiu/subscriptions/notify
PHR App-->>ABDM Gateway:s
{{< /mermaid >}}