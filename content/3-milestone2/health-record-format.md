+++
title = "Health Record Formats"
date = 2023-04-03T04:10:00+05:30
weight = 1
chapter = true
pre = "<b>3.1 </b>"
+++

# Health Record Formats

ABDM accepts only the documents that adhere to the FHIR's (Fast Healthcare Interoperability Resources) Implementation Guidelines.

Here is a list of Health Records, based on **FHIR's specifications:**

|Name|Definition|
|----|---------------|
Diagnostic Report Record|	The Clinical Artifact represents diagnostic reports including Radiology and Laboratory reports that can be shared across the health ecosystem.
Discharge Summary Record|Clinical document used to represent the discharge summary record for ABDM HDE data set.
Health Document Record|The Clinical Artifact represents the unstructured historical health records as a single of multiple Health Record Documents generally uploaded by the patients through the Health Locker and can be shared across the health ecosystem.
Immunization Record|The Clinical Artifact represents the Immunization records with any additional documents such as vaccine certificate, the next immunization recommendations, etc. This can be further shared across the health ecosystem.
OP Consult Record	| The Clinical Artifact represents the outpatient visit consultation note which may include clinical information on any OP examinations, procedures along with medication administered, and advice that can be shared across the health ecosystem.
Prescription Record| The Clinical Artifact represents the medication advice to the patient in compliance with the Pharmacy Council of India (PCI) guidelines, which can be shared across the health ecosystem.
Wellness Record|The Clinical Artifact represents regular wellness information of patients typically through the Patient Health Record (PHR) application covering clinical information such as vitals, physical examination, general wellness, women wellness, etc., that can be shared across the health ecosystem.


