+++
title = "Health Record Formats"
date = 2023-04-03T04:10:00+05:30
weight = 1
chapter = true
pre = "<b>3.1 </b>"
+++

# Health Record Formats

HRP can only link the following type of health records to an ABHA Address. All health records must be structured as FHIR (Fast Healthcare Interoperability Resources) formats. The FHIR specifications used by ABDM are published and maintained by the National Resource Centre for E-Health Standards (NRCES) at [https://nrces.in/ndhm/fhir/r4/index.html](https://nrces.in/ndhm/fhir/r4/index.html). 

All health records have been designed to be used in 2 ways 

- A simple FHIR bundle with a PDF or image attachment containing the detailed health information
- A structured FHIR bundle with coded health information. 

While integrators can start with simple bundles with attachments, they will be expected to comply with producing structured FHIR data within a couple of years from achieving compliance. 

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

