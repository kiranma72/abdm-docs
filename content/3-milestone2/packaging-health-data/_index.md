+++
title = "Packaging Health Data"
date = 2023-05-18T05:10:00+05:30
weight = 7
chapter = true
pre = "<b>3.7 </b>"
+++

# Packaging Health Data

This section helps you understand data packaging, what goes into the main envelope, types of health information and much more. The examples provided in this section only explain the syntactic means of the data formats. For expressing symantec meaning via standards, encoding and terminologies please refer to the CDAC NRCeS website or as recommended by NHA.

**Developers resource**

- You will need to use an FHIR client library to code the JSON samples provided in the sections below. Please refer to the FHIR references for developers and implementers at this link.
- During development, it's usually a good idea to validate the resource. For this, you may use one of the validators listed in the reference [library/resources](https://sandbox.abdm.gov.in/docs/resources) section. For example, the following example validates the entire file content (json)

**FHIR Documents**

- As explained in the APIs and Standards section, the following are the Health Information (HI) Types that are currently supported. The document type codes must be specfied as per the defined SNOMED-CT codes specified below. Please check the "Main Envelope" section to see example.

Code | Display | SNOMED-CT code
|---|-----|---------|
Prescription	|Prescription|	440545006
DiagnosticReport	|Diagnostic Report|	721981007
OPConsultation	|OP Consultation|	371530004
DischargeSummary	|Discharge Summary|	373942005
ImmunizationRecord	|Immunization Record|	41000179103
HealthDocumentRecord	|Record artifact|	419891008
WellnessRecord	|Wellness Record|	N/A (Should match exact text Wellness record)

- Please refer to NRCeS' [Implementer's Guide](https://nrces.in/ndhm) to create FHIR documents compliant to the FHR standards.

**This section covers**

{{% notice %}}
- The main envelope
- Diagnostic reports as FHIR DiagnosticReport
- Data encryption and decryption
- How to start testing the health repositories
{{% /notice %}}







