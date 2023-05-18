+++
title = "Diagnostic Reports"
date = 2023-05-18T05:10:00+05:30
weight = 2
chapter = true
pre = "<b>3.7.2 </b>"
+++

# Diagnostic Reports as FHIR DiagnosticReport

You may send more structured information for a Diagnostic Report (advised), by using the FHIR DiagnosticReport resource. Typically the most important elements of DiagnosticReports are:

1. **code:** The examples given below show only textual element 'text', but you may use 'Coding' along with 'display' element expressing a human readable name.
2. **issued:** Date and time when the report was issued, usually after the report was reviewed and verified. It's the date on which the pathologist or radiologists signs the document.
3. **results:** When you want to express the result observation in greater detail. You may also use the 'conclusion' parameter. Note in the example below how the 'results' are references to 'observations' within the same bundle.
4. **conclusion:** Clinical conclusion (interpretation) of test results.
5. **presentedForm:** An [attachment](https://www.hl7.org/fhir/datatypes.html#Attachment, which contains the entire project. It can be a pdf, image, or even a dicom file.
6. **media:** When you want to send over images associated with this report, such as imaging test results and radiological reports. 
7. **imagingStudy:** Reference to full details of imaging associated with the diagnostic report. Used for advanced radiology reporting with details of study, series and instances. In the reference stack, we do not support ImagingStudy yet; we use the 'media' tag in association with the specific 'category' to interpret as radiology results.
8. **category:** A service category that classifies the discipline, department or diagnostic service that created the report (for example, cardiology, biochemistry, hematology, radiology). Reference stack utilizes this element to interpret radiology results, although you may very well adopt a strategy by detecting the 'coding' tag assigned to the 'code'. This is probably quite impossible unless the affinity domain agrees on the clinical terminologies and coding standards to adopt. We think category is a decent start when such standardization is not possible to begin with.

**Important:** You must send either of the 'results' tag, or 'presentedForm' or the 'media' tag in the DiagnosticReport.

---

## FHIR Bundle (Sample)

1. View Prescription Document from [here](https://sandbox.abdm.gov.in/bundles/PrescriptionDoc.json)
2. View Discharge summary Document from [here](https://sandbox.abdm.gov.in/bundles/DischargeSummaryDoc.json)
3. View Immunization Document from [here](https://sandbox.abdm.gov.in/bundles/ImmunizationDoc.json)
4. View Health Record Document from [here](https://sandbox.abdm.gov.in/bundles/HealthDocumentRecordDoc.json)
5. View Wellness Record Document from [here](https://sandbox.abdm.gov.in/bundles/WellnessRecordDoc.json)
6. View Diagnostic Report Document from [here](https://sandbox.abdm.gov.in/bundles/DiagnosticReportDocument.json)
7. View Consultation Document from [here]https://sandbox.abdm.gov.in/bundles/ConsultationDoc.json

---

## Simple pathology report

In the following code snippet, we're showing you a basic pathological test example. We will then get on with explaining other types of tests. The following snippet describes how you can convey the Hemoglobin level of an individual.

```json

{
  "resourceType": "Bundle",
  "id": "ff626758-73cc-4821-978a-2528bb65b918",
  "meta": {
    "lastUpdated": "2019-01-03T15:32:26.605+05:30"
  },
  "timestamp": "2019-01-03T15:32:26.605+05:30",
  "identifier": {
    "system": "https://www.your-hospital.in/bundle",
    "value": "ff626758-73cc-4821-978a-2528bb65b918"
  },
  "type": "document",
  "entry": [
    {
      "fullUrl": "Composition/1007DR1",
      "resource": {
        "resourceType": "Composition",
        "id": "1007DR1",
        "date": "2019-01-03T15:32:26.605+05:30",
        "text": {
          "status": "generated",
          "div": "<div xmlns="http://www.w3.org/1999/xhtml">Diagnostic Report for Navjot Singh (RVH1002) </div>"
        },
        "identifier": {
          "system": "https://www.max.in/composition",
          "value": "1007DR1"
        },
        "status": "final",
        "type": {
          "coding": [
            {
              "system": "https://ndhm.gov.in/sct",
              "code": "721981007",
              "display": "Diagnostic Report"
            }
          ],
          "text": "Prescription record"
        },
        "encounter": {
          "reference": "Encounter/7fce6ec8-5013-4a27-b0a6-c43232608cda",
          "display": "OPD Visit - patient walked in"
        },
        "subject": {
          "reference": "Patient/RVH1002"
        },
        "author": [
          {
            "reference": "Organization/MaxSaket01"
          },
          {
            "reference": "Practitioner/DHID1234"
          }
        ],
        "title": "Doc: Surgical Pathology Report",
        "section": [
          {
            "title": "Section - Diagnostic report: Surgical Pathology",
            "code": {
              "coding": [
                {
                  "system": "https://ndhm.gov.in/sct",
                  "code": "721981007",
                  "display": "Diagnosti Report: Surgical Pathology"
                }
              ]
            },
            "entry": [
              {
                "reference": "DiagnosticReport/a45840dc-cf6b-4fcc-acec-d54a3bea40ff"
              }
            ]
          }
        ]
      }
    },
    {
      "fullUrl": "DiagnosticReport/a45840dc-cf6b-4fcc-acec-d54a3bea40ff",
      "resource": {
        "resourceType": "DiagnosticReport",
        "id": "a45840dc-cf6b-4fcc-acec-d54a3bea40ff",
        "status": "final",
        "code": {
          "text": "Surgical Pathology Report"
        },
        "subject": {
          "display": "Navjot Singh",
          "reference": "Patient/RVH1002"
        },
        "performer": [
          {
            "reference": "Organization/MaxSaket01"
          }
        ],
        "resultsInterpreter": [
          {
            "reference": "Practitioner/DHID1234"
          }
        ],
        "result": [
          {
            "reference": "Observation/fa357bd6-7107-4938-91fa-3da1815dea93"
          }
        ],
        "effectiveDateTime": "2019-01-03T17:32:26.605+05:30",
        "issued": "2019-01-03T18:32:26.605+05:30",
        "conclusion": "Refer to Doctor. To be correlated with further study."
      }
    },
    {
      "fullUrl": "Observation/fa357bd6-7107-4938-91fa-3da1815dea93",
      "resource": {
        "resourceType": "Observation",
        "id": "fa357bd6-7107-4938-91fa-3da1815dea93",
        "status": "final",
        "code": {
          "text": "Hemoglobin"
        },
        "valueString": "14 g/dL"
      }
    }
  ]
}
```

**Explanation:**

1. **results :** The DiagnosticReport resource has a 'results' tag that refers to another resource within the 'bundle'. Also note the usage of reference (Observation/ id ), specifically the id to resolve the other resource's reference in the same bundle. All such resource references must be resolvable within the same bundle and usage of Id is advised.
2. **FHIR references can even be an Http URL :** Do not send over such URL reference.
3. **conclusion :** This tag is optional. Typically a lab would send over the 'impression' tag and not the conclusive result.

---

## Simple pathology report (Attachment)

Here's what you do if you want to send over a PDF report of a blood test:

```json

{
  "resourceType": "Bundle",
  "id": "9473cf69-9fb8-4551-908f-94d0e081b9cc",
  "type": "document",
  "entry": [
    {
      "fullUrl": "Composition/1007DR1",
      "resource": {
        "resourceType": "Composition",
        "id": "1007DR1",
        "date": "2019-01-03T15:32:26.605+05:30",
        "text": {
          "status": "generated",
          "div": "<div xmlns="http://www.w3.org/1999/xhtml">Diagnostic Report for Navjot Singh (RVH1002) </div>"
        },
        "identifier": {
          "system": "https://www.max.in/composition",
          "value": "1007DR1"
        },
        "status": "final",
        "type": {
          "coding": [
            {
              "system": "https://ndhm.gov.in/sct",
              "code": "721981007",
              "display": "Diagnostic Report"
            }
          ],
          "text": "Prescription record"
        },
        "encounter": {
          "reference": "Encounter/7fce6ec8-5013-4a27-b0a6-c43232608cda",
          "display": "OPD Visit - patient walked in"
        },
        "subject": {
          "reference": "Patient/RVH1002"
        },
        "author": [
          {
            "reference": "Organization/MaxSaket01"
          },
          {
            "reference": "Practitioner/DHID1234"
          }
        ],
        "title": "Doc: Surgical Pathology Report",
        "section": [
          {
            "title": "Diagnostic report: CBC",
            "code": {
              "coding": [
                {
                  "system": "https://ndhm.gov.in/sct",
                  "code": "721981007",
                  "display": "Diagnosti Report: Complete Blood Count"
                }
              ]
            },
            "entry": [
              {
                "reference": "DiagnosticReport/a45840dc-cf6b-4fcc-acec-d54a3bea40ff"
              }
            ]
          }
        ]
      }
    },
    {
      "fullUrl": "DiagnosticReport/a45840dc-cf6b-4fcc-acec-d54a3bea40ff",
      "resource": {
        "resourceType": "DiagnosticReport",
        "id": "a45840dc-cf6b-4fcc-acec-d54a3bea40ff",
        "status": "final",
        "code": {
          "text": "Complete Blood Count Panel"
        },
        "effectiveDateTime": "2019-11-03T00:00:00+00:00",
        "issued": "2019-11-05T00:00:00+00:00",
        "presentedForm": [
          {
            "contentType": "application/pdf",
            "data": "base64 encoded inline data",
            "title": "Complete Blood Count (CBC)"
          }
        ]
      }
    }
  ]
}
```

**Explanation:**

1. **presentedForm:** You can transfer any type of attachment using this tag. The 'contentType' tag describes the mime type of the content. Display of the mimetype depends on the HIU's viewer device. However, try and stick to the following:
	- application/pdf
	- image/jpeg
	- image/png
	- application/msword
	- application/rtf, 
	- audio/mpeg
2. **data:** This is the base64 encoded inline data of the attachment. In many ways, it's like the [Media resource](https://github.com/ProjectEKA/projecteka.github.io/wiki/PHR-FHIR-Envelope) discussed earlier.

Note for simplicity sake, the example above does not illustrate the full document details like the Practitioner, Patient, Organization etc. They must be included in the document and should be resolvable by the references


