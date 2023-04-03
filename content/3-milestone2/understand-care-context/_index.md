+++
title = "Understand Care Context"
date = 2023-04-03T04:10:00+05:30
weight = 2
chapter = true
pre = "<b>3.2 </b>"
+++

# Understand Care Context

The idea of **Care Context** is to create a logical bundle of the health records. Each HMIS/LMIS system must decide how they want to organise data in care context.

**Our recommendations:**
- One care context for every outpatient visit & 1 care context for inpatient visit.
- Every care context has a reference ID, and a display name. The reference ID is internal to the hmis/lmis system & must be used to identify the set of health records associated with the care context.
- The display name can contain info that helps the user identify which records are included but must not contain any confidential information or test results.
- Example: OPD records (XRay, Prescription) from 3rd March 2023


The discovery process occurs when a consent manager sends out a request to the concerned HIP to identify the patient in the HIP system.

1. As part of the discovery request, the HIP will receive a list of verified identifiers along with name and demographic information, for example, the patient's mobile number, name, gender, year of birth and patient Id.
2. The matching logic is as depicted in the flowchart below and also in API specifications:
Note: Look for APIs with tag discovery and link

![Discovery Linking Flowchart](/abdm-docs/img/DiscoveryLinking.png)

3. As response to the discovery request, the HIP must send several masked details, as follows:
	- Patient reference: MHCXX111 - typically the identifier for the patient at the HIP.
Display: A description of the patient, comprising of the following information:
		- Name: John Doe
		- Email id: johndoe@example.com
		- Minor: Mother's name is Jane Doe
	Refrain from providing any critical information in the display area.
	- For the patient, you need to send one or more care-context detail, as follows:
		- Care context reference: ABXXX222
		- Display: General diagnosis
	Provide only a general hint of the patient's care context here, staying away from private diagnostic details. Here's an example:
		- TB program: Use your Nikshay program ID
		- PMJAY program: This context is linked with your PMJAY ID - PXXX239
		- Your last visit was with Dr. Shekhar on 21/03/2020
		- This is a child's immunization program

![Link Record Step 3](/abdm-docs/img/linkrecord-Step3.png)

4. Hospitals group patient data in the form of care context. Think of care-context as information about an association of a patient with an HIP for a period of time under which related healthcare activities may occur. Grouping of the care context can be based on the following:
	- Program-based: A patient visiting a hospital can sign up for any program, and belong to multiple programs as well. This kind of grouping is done generally in hospitals which deal with care programs for multiple ailments and specialities such as the general checkup service, cancer program, maternity care and so on.
	- Visit-based: Patient record can be tagged as inpatient, outpatient, or emergency, based on the purpose of the patient's visit.
	- Episode of Care: Some hospitals are capable of grouping patient records by the specific episode of care
	- Department-based: Patient records can be tagged by department as well, especially in large general hospitals.

