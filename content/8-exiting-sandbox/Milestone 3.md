+++
title = " Milestone 3"
date = 2023-03-13T14:30:25+05:30
weight = 7
chapter = true
pre = "<b>10.3</b>"
+++

# Milestone 3

**Functionalities of Milestone 3:** Developing Health Information User (HIU) services to provide view of patient’s medical history to authorized healthcare workers with complete consent.


S.No|Function|Functionality|Test Case|Steps To Be Executed 
|--|----|------|-----|-----|
1.1|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Patient Discovery HIU_FLOW_101|The System should have a provision to find the patient using ABHA Number or ABHA Address.|1. Enter ABHA Address/ ABHA Number 2. Select Find Patient
1.2|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Consent Request Initiation HIU_FLOW_102|HIU creates consent request for health records|1. Enter purpose for consent request. 2. Enter duration and expiry of consent request. 3. Enter Health Info type (out of 7 Health Info types). 4. Initiate Request
1.3|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Listing of Consent Requests HIU_FLOW_104|The system should be able to view the list of consent requests inititated|1. List of Consent Requests should include - ABHA| date of creation| date of expiry and Status of request
1.4|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Consent Request is Denied HIU_FLOW_105|The HIU system should not fetch health data for a denied consent request|1. Deny Consent Request on PHR App. 2. Check if data is accessible on the HIU application.
1.5|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Consent Request is Approved HIU_FLOW_106|The HIU system would fetch health data for the approved consent request
1.6|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_107|Fetch health data for (HI Type = DiagnostocReport Structured/Un-Structured)|1. Approve Consent Request on PHR App. 2. Check if data is accessible on the HIU application
1.7|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_108|Fetch health data for (HI Type = Prescription-Structured)|1. Approve Consent Request on PHR App. 2. Check if data is accessible on the HIU application
1.8|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_109|Fetch health data for (HI Type = DischargeSummary-Structured)|1. Approve Consent Request on PHR App. 2. Check if data is accessible on the HIU application
1.9|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_110|Fetch health data for (HI Type = CosultingNote-Structured)|1. Approve Consent Request on PHR App. 2. Check if data is accessible on the HIU application
1.10|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_111|Fetch health data for (HI Type = Immunization record-Structured)|1. Approve Consent Request on PHR App. 2. Check if data is accessible on the HIU application
1.11|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_112|Fetch health data for (HI Type = Health Record-Structured)|1. Approve Consent Request on PHR App 2. Check if data is accessible on the HIU application
1.12|Create Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}   HIU_FLOW_113|Fetch health data for (HI Type = Wellness Record-Un-Structured)|1. Approve Consent Request on PHR App. 2. Check if data is accessible on the HIU application
2.1|Revoke Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Revoke Consent HIU_FLOW_202|HIUs should not be able to view health records if the consent is revoked.|1. Check list of consent requests to view revoked consents. 2. Check if health record is visible in case the consent is revoked.
3.1|Expiry of Consent Request|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Consent Expiry HIU_FLOW_301|The HIU should not be able to view the health data of an expired consent request|1. Provide consent with a short expiry period. 2. Check status of consent after expiry. 3. Check if health record is visible to HIU after consent expiry