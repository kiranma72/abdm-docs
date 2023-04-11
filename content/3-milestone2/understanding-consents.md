+++
title = "Understanding Consents"
date = 2023-04-10T05:10:00+05:30
weight = 4
chapter = true
pre = "<b>3.4 </b>"
+++

# Understanding Consents

- ABDM design is aligned with **India's Personal Data Protection Bill,** that is the exchange of health data can only happen with the consent of the User.

- The entity requesting access to the data (HIU), needs to provide the following information:
	1. The purpose for which they want access to data
	2. The historical time period of health data
	3. The type of health records
	4. How long they wish to keep a copy the data

- ABDM uses an electronic consent artefact based on [**MEITY's electronic consent framework**](https://dla.gov.in/sites/default/files/pdf/MeitY-Consent-Tech-Framework%20v1.1.pdf) to allow HIUs to specify their consent request.

- Users can modify any of the request consent parameters, and provide a consent approval that suits them.

- Users have the option to revoke the consent they have provided to the HIU, at any time. The HIU must remove any copy of the users' data when the consent is revoked.

- All HIPs who are holding any data associated with this consent are notified. They must save a copy of the consent artefact in their system. Data can be shared against this consent any number of times till the consent expires / is revoked by the user.
![Understanding Consents](../understanding-consents.jpg)

### Making a consent request (as HIU)

An HIU can create a request to obtain a patient's consent to access her health information, as follows:

1. As an HIU, you will need to log in to sandbox's reference doctor's interface with login credentials (this will be sent to you via email). If you don't have your login credentials, Send a Request to Integrate Your Test Environment to NHA. NHA will respond along with your login credentials.
2. After logging in, you can create the consent request by providing the following details:
	- User's consent manager ID
	- Purpose of your consent request
	- Details of who is requesting the health information
	- The time period for which you require the patient's health documents. This information will enable your HIP to share the patient's health documents relevant to the required time period.
	- Provide a list of the health information types for which you're requesting, such as clinical notes, examination data and so forth.
3. Your consent request as HIU comes with a consent expiry time, after which you will not be able to access the patient's data.

### Receiving a consent artefact (as HIP)

The HIP receives the consent artefact after patients grants a request. The consent artefact lets the HIP know what data needs to be shared, as detailed below:

1. Patient's consent manager ID
2. Purpose of data access consent
3. Details of who is requesting the health information and of whom
4. Health information types; the HIP needs to maintain details of what has been requested and what has been sent, as detailed in the following table:

What is requested?|What needs to be sent?
|---|--------|
Prescription|Medicaton that the doctor advised
Diagnostic Report|Diagnostic Report that was created following a test/procedure
OP Consultation|Out Patient Consultation Document which may include complaints, prescription, observations, follow ups, appointments, test reports etc
Discharge Summary|Discharge Summary document which may include conditions, medications, observations, procedure done, discharge note, treatment plan etc
Immunization Record|Immunization records with any additional documents such as vaccine certificate, the next immunization recommendations, etc.
Record artifact|Unstructured historical health records as a single of multiple Health Record Documents generally uploaded by the patients through the Health Locker and can be shared across the health ecosystem.
Wellness Record|Regular wellness information of patients typically through the Patient Health Record (ABHA) application covering clinical information such as vitals, physical examination, general wellness, women wellness, etc.

*Note: For detailed information on what information can be sent for a requested HI Type, please refer to the Data Format Specifications*

5. The consent request is time-bound; after time is elapsed the HIU cannot view the data once the user has granted and HIP should check this date before sending any data.

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
PATRQT|Self Requested|Only applicable if patient herself is requesting information

## JSON Structure of COnsents

- Request data with signed consent

```JSON
{
  "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
  "timestamp": "1970-01-01T00:00:00.000Z",
  "notification": {
    "status": "GRANTED",
    "consentId": "1876f69b-c9c0-4000-88a4-01933ae7df01",
    "consentDetail": {
      "schemaVersion": "",
      "consentId": "1876f69b-c9c0-4000-85e5-f8d1a5f1a701",
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
        "text": "string",
        "code": "string",
        "refUri": "http://example.com"
      },
      "hip": {
        "id": "string",
        "name": "TESI-HIP"
      },
      "consentManager": {
        "id": "string"
      },
      "hiTypes": [
        "OPConsultation"
      ],
      "permission": {
        "accessMode": "VIEW",
        "dateRange": {
          "from": "1970-01-01T00:00:00.000Z",
          "to": "1970-01-01T00:00:00.000Z"
        },
        "dataEraseAt": "1970-01-01T00:00:00.000Z",
        "frequency": {
          "unit": "HOUR",
          "value": 0,
          "repeats": 0
        }
      }
    },
    "signature": "Signature of CM as defined in W3C standards; Base64 encoded",
    "grantAcknowledgement": false
  }
}
```

