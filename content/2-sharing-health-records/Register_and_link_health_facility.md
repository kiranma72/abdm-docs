---
title: "Link Health Facilities with HRP"
date: 2022-05-07T18:00:04+05:30
Weight: 5 
pre: "<b>2.6 </b>"
draft: false
---


# Register the health facility that uses your software and link it to your software endpoint

Following article focuses on HMIS/LMIS/HRPs software providers can register the facilities which uses their softwares

All integrators are expected to first ensure their systems work correctly on sandbox before migrating to production.

#### On-boarding a Facility into a HFR:
ABDM will support 2 methods to onboard health facilities

##### Method 1: Facility Manager registers via HFR Portal
Health facility should sign up on the Health Facility Registry and then link the ABDM compatible HRP software it plans to use.

For Registration, please follow instructions in this [PDF](/abdm-docs/img/HFR%20Registration%20Flow.pdf).

Once HFR Id is received, show process fof linking a facility with HRP s/w using HFR UI. (Check with Anshul)

##### Method 2: HIMS/LIMS Provider declares facility that uses their Softwares

This is a new process where the HRP can declare the presence of the health facility in the Health Facility registry (HFR) via an API or by Bulk Upload. 

Every HIMS/LIMS provider (HRP) must first register a Nodal contact as a Facility Manager and obtain a HPID.

To obtain HPID for a Nodat Contact, please [click here](https://hprid.ndhm.gov.in/register).

Ensure that HPID is created by using Password.
Ensure that Client ID is enabled with the HPID role. (How to check role is assign link)
To get the role added to ypur Client ID send an email request to abdm.support@nha.gov.in

Step 1: Get a Session Token with your Client ID/Secret
(Link to /abdm-docs/1-basics/sandbox_request_status_page/)

Step 2: Authenticate your HPID using the passowrd

https://hpridsbx.abdm.gov.in/api/swagger-ui.html#/. Expand the “Authentication” tab and select “/v1/auth/authPassword” API (Add API response here and proper API)

Step 3: Declare the facility using CREATE API

Add Create facility API

The create API performs a search to see if the facility being registered is a possible duplicate. The search gets a list of facilities for the same State, District, PINCODE, facility ownership and then checks the levenshtein distance between the facility name and all registered facilities. The API call will fail if the levenshtein distance is less than 4 for any existing facility. If you are unable to register a facility and believe it is not a duplicate entry please write to integration.support@nha.gov.in

Step 4: Link a declared Facility with your hosted endpoints
