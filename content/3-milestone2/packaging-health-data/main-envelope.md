+++
title = "Main Envelope"
date = 2023-05-18T05:10:00+05:30
weight = 1
chapter = true
pre = "<b>3.7.1 </b>"
+++

# Main Envelope

The base **FHR envelope** contains all the data that you want to transfer, compiled as a FHIR Bundle. A FHIR Bundle, referred to as data content, allows for packaging information of multiple types or as a Document.

- You can send over multiple such bundles through the data transfer API.
- Note that the bundle itself must be encrypted.

**Note:** Refer to the API reference documentation for information on bundles and how data should be sent over HTTPs. For bundle encryption, refer to the API and Elliptic-curve Diffie–Hellman key exchange documentation.

The following is a sample of the basic structure of a FHIR Bundle:

```json

{
  "resourceType": "Bundle",
  "id": "bundle01",
  "meta": {
    "versionId": "1",
    "lastUpdated": "2020-01-01T15:32:26.605+05:30"
  },
  "timestamp": "2020-01-01T15:32:26.605+05:30",
  "identifier": {
    "system": "https://example.hospital.com/pr",
    "value": "bundle01"
  },
  "type": "document",
  "entry": [
    {
      "fullUrl": "Composition/1",
      "resource": {
        "resourceType": "Composition",
        "id": "1",
        "date": "2020-01-01T15:32:26.605+05:30",
        "meta": {
          "versionId": "1",
          "lastUpdated": "2020-01-01T15:32:26.605+05:30"
        },
        "identifier": {
          "system": "https://example.hospital.com/documents",
          "value": "645bb0c3-ff7e-4123-bef5-3852a4784813"
        },
        "status": "final",
        "type": {
          "coding": [
            {
              "system": "https://ndhm.gov.in/sct",
              "code": "440545006",
              "display": "Prescription record"
            }
          ],
          "text":"Prescription Record"
        },
        "subject": {
          "reference": "Patient/1",
          "display": "Hina Patel"
        },
        "author": [
          {
            "reference": "Practitioner/1",
            "display": "Dr. Manju Sengar"
          }
        ],
        "title": "Prescription record",
        "encounter": {
          "reference": "Encounter/7fce6ec8-5013-4a27-b0a6-c43232608cda",
          "display": "OP Visit"
        },
        "attester": [
          {
            "mode": "official",
            "time": "2019-01-04T09:10:14Z",
            "party": {
              "reference": "Organization/MaxSaket01",
              "display": "Max Super Speciality Hospital, Saket"
            }
          }
        ],
        "section": [
          {
            "title": "Prescription record",
            "code": {
              "coding": [
                {
                  "system": "https://affinitydomain.in/sct",
                  "code": "440545006",
                  "display": "Prescription record"
                }
              ]
            },
            "entry": [
              {
                "reference": "MedicationRequest/1"
              }
            ]
          }
        ]
      }
    },
    {
      "fullUrl": "Organization/MaxSaket01",
      "resource": {
        "resourceType": "Organization",
        "id": "MaxSaket01",
        "name": "Max Super Speciality Hospital, Saket",
        "identifier": [
          {
            "type": {
              "coding": [
                {
                  "system": "http://terminology.hl7.org/CodeSystem/v2-0203",
                  "code": "PRN",
                  "display": "Provider number"
                }
              ]
            },
            "system": "https://facility.ndhm.gov.in",
            "value": "10000005"
          }
        ],
        "address": [
          {
            "line": [
              "1, 2, Press Enclave Marg, Saket Institutional Area, Saket"
            ],
            "city": "New Delhi",
            "state": "New Delhi",
            "postalCode": "110017",
            "country": "INDIA"
          }
        ]
      }
    },
    {
      "fullUrl": "Encounter/7fce6ec8-5013-4a27-b0a6-c43232608cda",
      "resource": {
        "resourceType": "Encounter",
        "id": "7fce6ec8-5013-4a27-b0a6-c43232608cda",
        "status": "finished",
        "class": {
          "system": "http://terminology.hl7.org/CodeSystem/v3-ActCode",
          "code": "AMB",
          "display": "Outpatient visit"
        }
      }
    },
    {
      "fullUrl": "MedicationRequest/1",
      "resource": {
        "id": "1",
        "resourceType": "MedicationRequest",
        .....
      }
    }
  ]
}
```

**Explanation:**

- resourceType*: It must be Bundle
- id*: Id must be unique for each bundle that you want to send. For traceability purposes, it's recommended that you provide an id (for every resource) that you must be able to resolve within your system.
- timestamp*: Timestamp should be the time of issue of the document.
- identifier*: It should be an identifier by which you can trace the document back to your system
- type*: Type must be "document". The first resource must be a composition in the bundle, and is meant for contextual grouping of information.
- entry*: It is an array of FHIR resources. As of now, the reference HIU service supports top level Health Information (HI) types like - "Prescription", "Diagnostic Report", "Discharge Summary", "OP Consultation", which may contain resources like "Observation", "Condition", "MedicationRequest", "DocumentReference", "DiagnosticReport", "Procedure" - and also other reference entities like "Medication", "Practitioner", "Patient", "Organization", etc.
- meta.versionId : The versionId should be mentioned in the bundle.meta . Can be used to ensure that updates are based on the latest version of the resource.

**Note** for simplicity sake, the example above does not illustrate the full document details like the Practitioner, Patient, Organization etc. They must be included in the document and should be resolvable by the references.

**Composition**

The composition is the first resource in the bundle and acts as a .. logical package that provides a single coherent statement of meaning, establishes its own context and that has clinical attestation with regard to who is making the statement. It defines the structure and content necessary for a document. Note, it alone does not mean anything, but along with its sections and entries allow grouping and packaging of all other resources, which when referenced from Composition must be included as entries in the Bundle.

- title*: Must be provided and must broadly describe what the composition is about.
- title*: Should specify what the type of the document is. For example "440545006" is meant for "Prescription Record" is SNOMED-CT.
- encounter*: Provides the context of visit or clinical encounter.
- subject*: The patient reference. You can provide minimal information. You should also provide a "display" attribute (typically the name) for the subject.
- author*: Specifies the practitioner who is the author of the document. In some contexts, this may be an Organization resource reference as well. Again, please provide a "display" attribute as well.
- attester*: It is used to list out the practitioner or organization who has attested to the accuracy of the composition/document. These listed resources must be available within the same bundle. As specified in the example, the mode should be official. In party, provide the reference of organization resource.
The organization must have an identifier registered with ABDM facility registry. Organization.identifier.value value should be an HIP id registered with ABDM facility registry.
for production use, the organization identifier system must be [ABDM facility registry](https://facility.ndhm.gov.in/) while for sandbox it should be [ABDM sandbox facility registry.](https://facilitysbx.ndhm.gov.in/)
- section*: Sections and their entries are used to list out the top level resources the document is composed of. For example, in the example above, it may contain a list of MedicationRequest (even a DocumentReference or Binary containing an image). Note, do not include the referenced resources (e.g. Patient, Encounter, Practitioner etc) in the section.entry[] - such resources must be available in the bundle, but need not be included in the section.list[]

**Important**

- Notice each bundle entry's fullUrl: there are 2 ways to specify so.
	- Specified as "resource-type/id", as logical URL, and resolvable within the bundle. Each resource id must be also specified.
- All entries must be resolvable in the bundle.
- Please do not provide absolute URL for any references.

**Document Types**

In the above example, we are preparing a FHIR Document for Prescription Record. Composition.type indicates what is the document about, and you must send over the appropriate codes, so that the HIU or Patient applications understand the health information sent.

Just like in the example above, if you were to send over a Diagnostic Report Record you would send over **Composition.type** as:

```json

"type":{
  "coding":[
      {
        "system":"https://ndhm.gov.in/sct",
        "code":"721981007",
        "display":"Diagnostic Report"
      }
  ],
  "text":"Diagnostic Report Record"
}
```

