+++
title = "Notification to Mobile"
date = 2023-04-03T04:10:00+05:30
weight = 2
chapter = true
pre = "<b>3.3.2 </b>"
+++

# Notification to Mobile

**Applicable when:** User has come to the hospital, does not share ABHA address during registration but shares mobile, name, age, gender.

- Health Information Provider (HIP) calls an API with just the mobile number to notify the user that a new health record has been created for the patient.

- HIPs can send SMS to patients in case they have not registered and do not have a health-ID after their visit. HIPs will call gateway with phone number, care-context-details and an optional deeplink URL. 

## Sample User Experience

![sample user experienece](/abdm-docs/img/notification-to-mobile.png)

## Test Cases

**Function:** HIP Initiated Health Record Linking Using Mobile OTP

Functionality|Test Case|Steps To Be Executed 
|------|-----|-----|
{{% badge style="blue" %}}Mandatory{{% /badge %}} Link record via mobile OTP (HIP_INTI_LINK_201)|The system should have provision to link patient's Health record with ABHA address |1. Enter patient's ABHA address on the System. 2. OTP receive by the patient.
{{% badge style="blue" %}}Mandatory{{% /badge %}} OTP validation (HIP_INTI_LINK_203)|The user shares the OTP with the HIP for validation|1. Share Mobile OTP with HIP System. 2. Validate the OTP. 3. Upon successful validation of OTP| linking token is generated.
{{% badge style="blue" %}}Mandatory{{% /badge %}} Linking of Health Records (HIP_INTI_LINK_205)|HIP system links the ABHA Number / Address with the patient records|1. Link Health Records. 2. Through PHR Application| check if the linked records can be pulled


## API Sequence Diagram

The following flow diagram details the flows that take place during "Sending SMS to Patient" from the HIP perspective

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Notification to Mobile
HIP System->>Repository:POST/v0.5/patients/sms/notify
activate Repository
Repository->>Gateway:v0.5/patients/sms/notify
Gateway->>CM:Send SMS Request
CM->>Gateway:Send SMS Response
Gateway->>Repository:v0.5/patients/sms/on-notify
deactivate Repository
Repository->>HIP System:POST/v0.5/patients/sms/on-notify
{{< /mermaid >}}

## API Collection

