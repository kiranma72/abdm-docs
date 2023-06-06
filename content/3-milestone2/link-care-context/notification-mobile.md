+++
title = "Notification to Mobile"
date = 2023-04-03T04:10:00+05:30
weight = 2
chapter = true
pre = "<b>3.3.2 </b>"
+++

# Notification to Mobile

**Applicable when:** User does not share ABHA address during registration but shares mobile, name, age, gender.

- Health Information Provider (HIP) must call an ABDM API when a new health record is ready to be shared with an user. 
- ABDM sends the SMS to notify the user that they can access and link the new health record using any PHR app. 
- The SMS contains a deep link the triggers the PHR app. 
- The PHR app will help the user create an ABHA address, discover and link the health record. 

## Sample User Experience

![sample user experienece](/abdm-docs/img/notification-to-mobile.png)

## Test Cases

**Function:** HIP Initiated Health Record Linking Using Mobile OTP

Functionality|Test Case|Steps To Be Executed 
|------|-----|-----|
{{% badge style="blue" %}}Mandatory{{% /badge %}} Sending notification to the patient on their mobile with deep link (HIP_INIT_NOTIFY_HIECM)|HIP should notify HIE-CM when a new health record is generated & ABHA address is not available. This test case is applicable when patient has shared mobile number and has NOT shared ABHA address with HIP during patient registration. | **1.** New health record like Diagnostic report, Prescription, etc is created on EMR/HMIS system for a patient. <br/> **2.** Mobile number of patient is available in EMR/HMIS system  and ABHA address of the patient is NOT available in EMR/HMIS system.<br/> **3.** EMR/HMIS system will call the SMS/notify2 API on the gateway to inform of available of new health record (only the mobile number and the HIP ID is to be shared).<br/> **4.** ABDM should be sending notification to the patient on their mobile with deep link.<br/> **5.** Patient should be able to download/launch PHR app of their choice. <br/> **6.** PHR app will make a discovery request to the HIP.<br/> **7.** Care context for New patient record must be correctly discoverable in the PHR app.


## API Sequence Diagram

The following flow diagram details the flows that take place during "Sending SMS to Patient" from the HIP perspective

{{< mermaid >}}
%%{init:{"fontSize": "1.0rem", "sequence":{"showSequenceNumbers":true}}}%%
sequenceDiagram
title Notification to Mobile
HIP/HRP->>HIE-CM:POST/v0.5/patients/sms/notify
activate HIE-CM
actor User
HIE-CM->>User:Send SMS with deep link
HIE-CM->>HIP/HRP:v0.5/patients/sms/on-notify
{{< /mermaid >}}

## API Information Request Response 

**1. Send SMS Notifications**

API to send SMS notifications to patient with custom deeplink. "name" is the health facility name as in HFR and "id" is the HFR (HIP) ID. 

**BASE URL:** https://dev.abdm.gov.in/gateway

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/patients/sms/notify2$" >}}

**2. Acknowledgement Response For SMS Notification**

Acknowledgement response for SMS notification sent to patient by HIP

**BASE URL:** Callback URL registered for HRP

{{< swaggermin src="/abdm-docs/Yaml/ndhm-hip.yml" api="POST /v0.5/patients/sms/on-notify$" >}}