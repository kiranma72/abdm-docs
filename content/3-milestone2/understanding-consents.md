+++
title = "Understanding Consents"
date = 2023-04-10T05:10:00+05:30
weight = 4
chapter = true
pre = "<b>3.4 </b>"
+++

# Understanding Consents

ABDM was designed to align with India's **Personal Data Protection Bill,** that requires exchange of any personal data (like health data) to happen only with the consent of the User.

Any entity (Health Information User - HIU ) which would like to access health records that are linked to an ABHA address will require to first obtain a consent for data access. 

The HIU needs to create a consent request that contains the following information:

1. The purpose for which they want access to data
2. The historical time period of data they require
3. The type of health records (like diagnostics, prescriptions .. )
4. How long they wish to keep the copy of the data

ABDM uses an electronic consent artefact based on [**MEITY's electronic consent framework**](https://dla.gov.in/sites/default/files/pdf/MeitY-Consent-Tech-Framework%20v1.1.pdf) to specify consent requests.

On recieving a consent request, Users can review and also modify any of the request parameters, and provide a consent approval that suits them. for example they can change the type of records or the duration the HIU is allowed to keep the data. 

Once the user *grants* consent, the HIU will be able to use the signed consent artefact to get access to the health data

Users also have the option to *revoke* the consent they have provided to the HIU, at any time. The HIU must remove any copy of the user's data when the consent is revoked.

When a consent is granted or revoked by the user, The HIE-CM notifies all HIPs who holding any data associated with the consent. 

HRP/HIPs must save a copy of the consent artefact in their system when they get such a notification. 

HIUs can request Data using the signed consent any number of times till the consent expires / is revoked by the user.

The diagram below provides an overview of the consent based data sharing in ABDM 

![Understanding Consents](../understanding-consents.jpg)

### Working with Consents in the ABDM Sandbox

Developers can either use the [Sandbox Reference HIU](https://dev.ndhm.gov.in/hiu) or [Bahmini HIU](/abdm-docs/1-basics/bahmni/) to trigger consent requests. You can create a consent request against a Sandbox ABHA address (@ sbx), Grant / Deny / Revoke the request using the [Sandbox ABHA App](/abdm-docs/1-basics/sandbox_abha_app/) 

1. Login in to the HIU application. For the Sandbox reference HIU, If you don't have your login credentials, send a request with your client ID and email as outlined on the HIU page.  NHA will respond along with your login credentials.
2. After logging in, you can create the consent request including:
	- User's ABHA Sandbox address
  - Purpose of your consent request
	- Details of who is requesting the health information
	- The time period for which you require the patient's health documents. This information will enable your HIP to share the patient's health documents relevant to the required time period.
	- Provide a list of the health information types for which you're requesting, such as clinical notes, examination data and so forth.
3. Your consent request as HIU comes with a consent expiry time, after which you will not be able to access the patient's data.
4. Login to the Sandbox ABHA app with the ABHA address to which you raised the consent request 
5. Go to the requests tab to see the consent request and actions 
6. Make sure the ABHA address for which you are requesting consent has care contexts linked, ideally from a HIP that you have linked with your client id. 



### Meta Codes
While requesting and exchanging health information, there are few meta codes that are relevant to you if you are a HIU or HIP.

Purpose of Use - defines what is the purpose of use of the health information that a HIU is requesting for. The following are subset from http://terminology.hl7.org/ValueSet/v3-PurposeOfUse

Code|Display|Description
|--|----|-------|
CAREMGT|Care Management||
BTG|Break the Glass|Only applicable in extreme circumstances as override or provision of immediately needed health care for an emergent condition
PUBHLTH|Public Health||	
HPAYMT|Healthcare Payment|Typically for payers conducting financial or contractual activities related to payment for provision of health care
DSRCH|Disease Specific Healthcare Research||
PATRQT|Self Requested|Only applicable if patient himself/herself is requesting information

### Structure of Consent Request

```JSON
{
    "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
    "timestamp": "1970-01-01T00:00:00.000Z",
    "consent": {
        "purpose": {
            "text": "care management",
            "code": "CAREMGT",
            "refUri": "http://terminology.hl7.org/ValueSet/v3-PurposeOfUse"
        },
        "patient": {
            "id": "91686532731326@sbx"
        },
       
        "hiu": {
            "id": "HIU_2"
        },
        "requester": {
            "name": "Dr.Parthiban",
            "identifier": {
                "type": "REGNO",
                "value": "MH1001",
                "system": "https://www.mciindia.org"
            }
        },
        "hiTypes": [
            "OPConsultation",
            "Prescription"
        ],
        "permission": {
            "accessMode": "VIEW",
            "dateRange": {
                "from": "2020-11-25T12:30:29.592Z",
                "to": "2023-04-18T12:30:29.592Z"
            },
            "dataEraseAt": "2025-12-20T12:30:29.592Z",
            "frequency": {
                "unit": "MONTH",
                "value": 12,
                "repeats": 12
            }
        }
    }
}
```

### Notification of consent grant

```json
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "1970-01-01T00:00:00.000Z",
  "notification": {
    "status": "GRANTED",
    "consentId": "1876f659-bb20-4000-88dc-b45f97252901",
    "consentDetail": {
      "schemaVersion": "",
      "consentId": "1876f659-bb20-4000-83ff-489361a4bd01",
      "createdAt": "1970-01-01T00:00:00.000Z",
      "patient": {
        "id": "hinapatel79@ndhm"
      },
      "careContexts": [
        {
          "patientReference": "hinapatel79@hospital",
          "careContextReference": "Episode1"
        }
      ],
      "purpose": {
            "text": "care management",
            "code": "CAREMGT",
            "refUri": "http://terminology.hl7.org/ValueSet/v3-PurposeOfUse"
        },
      "hip": {
        "id": "string",
        "name": "TESI-HIP"
      },
      "consentManager": {
        "id": "sbx"
      },
      "hiTypes": [
        "OPConsultation"
      ],
      "permission": {
            "accessMode": "VIEW",
            "dateRange": {
                "from": "2020-11-25T12:30:29.592Z",
                "to": "2023-04-18T12:30:29.592Z"
            },
            "dataEraseAt": "2025-12-20T12:30:29.592Z",
            "frequency": {
                "unit": "MONTH",
                "value": 12,
                "repeats": 12
            }
        }
    },
    "signature": "Signature of CM as defined in W3C standards; Base64 encoded",
    "grantAcknowledgement": false
  }
}
```
