+++
title = "Fetch & Display Records"
date = 2023-05-02T03:53:25+05:30
weight = 10
chapter = true
pre = "<b>5.10 </b>"
+++

# Fetching and Display of Records

## Functionality Overview

- Every PHR Application also needs to implement an HIU (Health Information User)
- The process for implementing HIU is described in [**Milestone 3.**](/abdm-docs/4-milestone3/index.html)
- Whenever a new care context is linked to the ABHA address, the PHR App receives a notification.
- The PHR app is expected to **create a consent request** for that health record and send it to the HIE-CM.
- If auto-approval policy is in place, the consent is immediately approved.
- The PHR App must then initiate the health information request along with the consent to **obtain the health record from the HIP.**
- The PHR App must offer a long term storage for these health records for the user.
- The PHR app must **display the fetched records to the user** within the app organised ideally in chronological order.

## Test Cases

**Sharing of health records with patient's consent to the HIU** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = DiagnostocReport Structured)||||||||||||
2|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = DiagnostocReport Un-Structured)||||||||||||
3|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = Prescription-Structured)||||||||||||
4|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = Prescription-Un-Structured)||||||||||||
5|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = DischargeSummary-Structured)||||||||||||
6|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = DischargeSummary-Un-Structured)||||||||||||
7|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.(HI Type = CosultingNote-Structured)||||||||||||
8|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient. (HI Type = CosultingNote-Un-Structured)||||||||||||
9|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient. (HI Type = Immunization record-Structured)||||||||||||
10|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient. (HI Type = Immunization record-Un-Structured)||||||||||||
11|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient/ (HI Type = Wellness Record-Structured)||||||||||||
12|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient. (HI Type = Wellness Record-Un-Structured)||||||||||||
13|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient. (HI Type = Health Record-Structured)||||||||||||
14|{{% badge style="blue" %}}Mandatory{{% /badge %}}  HIU should be able to view the health data of a APPROVED consent request|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient.|Check whether HIU individual is able to fetch health data for the consent request created for a patient and APPROVED by the patient. (HI Type = Health Record-Un-Structured)

**Tabs in PHR app (My Records/Linked Facility/Consents)** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Requests" section in the "Consents" tab of PHR app|1) Requested - Not yet any action is taken by individual on consent request received from HIU to PHR app. |All request (consent / subscription / locker) sent by HIU to patiet are seen  in "Requested" dropdown within "Requests" section of PHR app
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Requests" section in the "Consents" tab of PHR app|2) Denied - Individual have "Denied" consent request received from HIU to PHR app. |All denied request (consent / subscription / locker) by patient are seen in "Denied" dropdown within "Requests" section of PHR app. 
3| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Requests" section in the "Consents" tab of PHR app|3) Expired -  Requests is expired because patient have not acted on consent request received in PHR app within the time duration set by HIU|All expired request (consent / subscription / locker) by patient are seen in "Expired" dropdown within "Requests" section of PHR app.
4| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Approved" section in the "Consents" tab of PHR app|1) Granted - Patient had granted the consent request received from HIU to PHR app|All granted request (consent / subscription / locker) by patient are seen in "Granted" dropdown within "Approved" section of PHR app. 
5| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Approved" section in the "Consents" tab of PHR app|2) Revoked - Patient had revoked consent requests after granting it in PHR app. |All revoked request (consent / subscription / locker) by patient are seen in "Revoked" dropdown within "Approved" section of PHR app. 
6| {{% badge style="blue" %}}Mandatory{{% /badge %}}  View patient helth records in "My Records" tab of PHR app|To view records, post linking and fetching from healthcare providers (health locker, health facility and health programme)|Click on record fetched in the "My Records" tab
7| {{% badge style="blue" %}}Mandatory{{% /badge %}}  View patient helth records in "My Records" tab of PHR app|To view records, post linking and fetching from healthcare providers (health locker, health facility and health programme) |Details of records are viewed with attachment
8| {{% badge style="blue" %}}Mandatory{{% /badge %}}  View patient helth records in "My Records" tab of PHR app|To view records, post linking and fetching from healthcare providers (health locker, health facility and health programme) |Click on the attachment to view the health record / report in the device
9| {{% badge style="blue" %}}Mandatory{{% /badge %}}  "Linked Facility" tab in PHR app| Linked providers includes health lockers| health facility and health programme|Ckeck list of all linked providers are displayed and "Pull Record" button is against each one of them. So that patient can click on it to fetch and view record in "My Records" tab.


