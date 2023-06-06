+++
title = "Understanding Care Contexts"
date = 2023-04-03T04:10:00+05:30
weight = 2
chapter = true
pre = "<b>3.2 </b>"
+++

## Understanding Care Contexts

A **Care Context** is a logical bundle of the health records. Each HMIS/LMIS system must decide how to organise data for a user into one or more care contexts. A care context is the element that is linked by the HMIS/LMIS with the ABHA address of the user. The HIE-CM is to be "data blind" by design, i.e. the HIE-CM should not have any visibility on the *content* of health records. The care context therefore has only 2 peices of information 

- A reference ID, this is an internal value that should be used by the HRP (HMIS/LMIS) to identify the health record that is part of this care context 
- A display name, this can contain info that helps the user identify which records are included but must not contain any confidential information or test results. For Example: "OPD records (XRay, Prescription) from 3rd March 2023"

We recommend that you can organize a users data into care contexts by creating
- One care context for every outpatient visit 
- One care context for each inpatient visit.

## JSON Structure of Care Contexts


```json
{
    "patient": {
      "referenceNumber": "TMH-PUID-001",
      "display": "TMH records for Kiran Kumar",
      "careContexts": [
        {
          "referenceNumber": "2375639",
          "display": "OPD records for O3 Oct 2022"
        },
        {
          "referenceNumber": "2375640",
          "display": "IPD records for admission betweenn O4 Oct 2022 to 06 Oct 2022"
        },
      ]
    }
}
```