



### Overview of the functionality:
- HIU can create a request to obtain a patient's consent to access  health information
- Consent request as HIU comes with a consent expiry time, after which you will not be able to access the patient's data.
- Patient grant or deny the consent request via PHR App
- The HIP/HRP receives the consent artefact after patients grants a request. Consent artefect saved in HIP/HRP end for future use.
- Approved/reject consent aretefect communicated to HIU


Obtaining the patient’s consent for information sharing begins when the HIU system issues a consent request to the consent manager for the patient’s data. The patient can view the request details, and choose to either grant consent or deny it. Patient can also 

The CM, notifies the HIU, and also sends a notification to the HIP of the patient’s consent if granted.

1: An HIU create a request to obtain a patient's consent to access her health information, as follows:

Consent request may have follwoing details:
- User's consent manager ID
- Purpose of your consent request
- Details of who is requesting the health information
- The time period for which you require the patient's health documents. This information will enable your HIP to share the patient's health documents relevant to the required time period.
- Provide a list of the health information types for which you're requesting, such as clinical notes, examination data and so forth.

Consent request as HIU comes with a consent expiry time, after which you will not be able to access the patient's data.

2: Patient Approved or reject the consent request via PHR App

3: CM notify to HIP/HRP after patient grant approval . HIP/HRP save the consent artefact after patients grants a request. The consent artefact lets the HIP know what data needs to be shared, as detailed below:

- Patient's consent manager ID
- Purpose of data access consent
- Details of who is requesting the health information and of whom
- Health information types; the HIP needs to maintain details of what has been requested and what has been sent.

4: Cosent manager sahre the approved consent artifect with HIU.

