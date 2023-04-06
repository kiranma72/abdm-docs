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

## JSON Structure of Care Context

## Grouping by care context
The definition and grouping by such 'care-context' is left entirely to the HIP. The information provided in the above section is meant only for guidance. Usually in EMR/EHR/PMS systems at hospitals, the systems index and patient records are filtered by patient-id and potentially grouped by any of the above means.

In terms of hierarchy, consider the following to understand how patients' records may be grouped in HIP systems.

1. Encounter or visit: This records the details of activity (one or more) directly relating to the patient. It is not advised to send specific clinical-encounters (single clinical-patient interaction) as care-context, unless you are sure that such recordings are going to be very limited.
2. Episode of care: This grouping means can link a series of encounters together in case of problems.
3. Program: This grouping can link a series of care episodes or visits. For example:
	- IMNCI (Integrated Management of Neonatal and Childhood Illness) as seen in various MCTS programs in Indian context
	- Vertical program specific like India's TB elimination program - Nikshay
	- National Noncommunicable diseases (NCD) program
	- National Health Mission (NHM)
	- Specific program targeted for Health and Wellness Centers

It is quite possible that a HIP system may not be capable of doing such grouping. In such cases only, consider using the same care-context reference that's assigned to patient reference in the HIP system.

The idea is to provide an aggregate or grouped means of patient's care settings at various healthcare centers. If proper care context grouping is not provided, patients who visit healthcare centers for different treatments will be forced to discover and link their care settings for each therapy or service.