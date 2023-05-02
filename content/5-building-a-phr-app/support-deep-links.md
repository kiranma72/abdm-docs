+++
title = "Support Deep links"
date = 2023-05-02T03:53:25+05:30
weight = 8
chapter = true
pre = "<b>5.8 </b>"
+++

# Support Deep Links

## Functionality Overview



## Test Cases

**Deep Link Flow** : Send SMS to patient mobile to initiate record linking and fetching in PHR app

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | In case patient visits the health facility and do not provide the ABHA address for linking of health records. Then, ABDM compliant health facility will notify ABDM when there is a new health record created of the patient. ABDM will send a deep link SMS is to the patient's mobile for fetching and viewing records in PHR app using User Initiated Linking Flow (Discovery Flow) | Patient visits a health facility and registers by providing Name, DoB, Gender and Mobile. Patient does not share any ABHA Address with the facility.
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | In case patient visits the health facility and do not provide the ABHA address for linking of health records. Then, ABDM compliant health facility will notify ABDM when there is a new health record created of the patient. ABDM will send a deep link SMS is to the patient's mobile for fetching and viewing records in PHR app using User Initiated Linking Flow (Discovery Flow) | If the Health Facility is participating in ABDM, then it will notify ABDM when there is a new health record for this patient. Only the mobile number and the ID of the facility is notified. Facilities are identified by the facility’s HIPCODE. This can be obtained by registering the facility using the Health Facility Registry and linking the facility to a ABDM approved Health Repository Provider Software.
3| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | In case patient visits the health facility and do not provide the ABHA address for linking of health records. Then, ABDM compliant health facility will notify ABDM when there is a new health record created of the patient. ABDM will send a deep link SMS is to the patient's mobile for fetching and viewing records in PHR app using User Initiated Linking Flow (Discovery Flow) | ABDM will send an SMS to the user with a deep link as shown below: Dear Madam/Sir, (facility name) is now participating in Ayushman Bharat Digital Mission (ABDM). Your report at this facility is now ready. See your record by clicking on on phr.abdm.gov.in/uhi/(hipcode) ABDM|NHA
4| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | In case patient visits the health facility and do not provide the ABHA address for linking of health records. Then, ABDM compliant health facility will notify ABDM when there is a new health record created of the patient. ABDM will send a deep link SMS is to the patient's mobile for fetching and viewing records in PHR app using User Initiated Linking Flow (Discovery Flow) |Clicking on the link will show the list of all ABDM compliant PHR applications.

**Post clicking on deep link by patient** 

Use Case 1: In case ABDM compliant PHR application is not installed in PHR app, then user is redirected to download and install it from play store/app store."

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | Post clicking on deep link by patient| Check that, if no ABDM compliant PHR application is installed in phone - Navigate patient to play store / app store to install the selected PHR application from the list of all ABDM compliant PHR applications. 
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | Post clicking on deep link by patient| Check that, post installing the PHR app. New user is able to create the ABHA address and Password by providing basic details such as Nma, DoB, Gender, Mobile No., Address 


Use Case 2: In case ABDM compliant PHR application is already installed in PHR app, then app will directly launch and initiate the User Initiated Linking (Discovery Flow)

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | Post clicking on deep link by patient| Check that selected PHR app from the list of all ABDM compliant PHR app's is launched successfully. 
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}   | Post clicking on deep link by patient| Check that post launch, PHR app initiates the discovery request with HIP where patient health records were created


## API Sequence Diagram


## API Collection

