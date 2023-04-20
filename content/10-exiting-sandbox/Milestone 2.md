+++
title = " Milestone 2"
date = 2023-03-13T14:30:25+05:30
weight = 6
chapter = true
pre = "<b>10.2</b>"
+++

# Milestone 2

**Description of Milestone 2**: Building Health Information Provider (HIP) services to share digital records via any Personal Health Records (ABHA) app. 

# Test Cases

Health Information Provider initiated for Health Records (Any of the 4 methods defined must be demonstrated for HIP Initiated Linking. It is recommended to implement all the 4 methods)

## Test Cases for Health Information Providers (HIP)

S.No|Function|Functionality|Test Case|Steps To Be Executed 
|--|----|------|-----|-----|
1.1|Health Record Creation|{{% badge style="blue" %}}Mandatory{{% /badge %}} Creation of Health Records (Health_RECORD_CREATION_101)|The system should have a provision to create digital health records|1. Check if digital Health Records are being created in HIP systems (valid for HI types as applicable to the integrating entity). 2.Recommend to have the health record in FHIR format.
2.1|HIP Initiated Health Record Linking Using Mobile OTP|{{% badge style="blue" %}}Mandatory{{% /badge %}} Link record via mobile OTP (HIP_INTI_LINK_201)|The system should have provision to link patient's Health record with ABHA address |1. Enter patient's ABHA address on the System. 2. OTP receive by the patient.
2.2|HIP Initiated Health Record Linking Using Mobile OTP|{{% badge style="blue" %}}Mandatory{{% /badge %}} OTP validation (HIP_INTI_LINK_203)|The user shares the OTP with the HIP for validation|1. Share Mobile OTP with HIP System. 2. Validate the OTP. 3. Upon successful validation of OTP| linking token is generated.
2.3|HIP Initiated Health Record Linking Using Mobile OTP|{{% badge style="blue" %}}Mandatory{{% /badge %}} Linking of Health Records (HIP_INTI_LINK_205)|HIP system links the ABHA Number / Address with the patient records|1. Link Health Records. 2. Through PHR Application| check if the linked records can be pulled
3.1|HIP Initiated Health Record Linking Using Aadhaar OTP|{{% badge style="blue" %}}Mandatory{{% /badge %}} Link record via aadhaar linked mobile  OTP (HIP_INTI_LINK_301)|The system should have provision to link patient's Health record with ABHA address |1. Enter patient's ABHA address on the System. 2. OTP receive by the patient.
3.2|HIP Initiated Health Record Linking Using Aadhaar OTP|{{% badge style="blue" %}}Mandatory{{% /badge %}} OTP validation (HIP_INTI_LINK_303)|The user shares the OTP with the HIP for validation|1. Share Mobile OTP with HIP System. 2. Validate the OTP. 3. Upon successful validation of OTP| linking token is generated."
3.3|HIP Initiated Health Record Linking Using Aadhaar OTP|{{% badge style="blue" %}}Mandatory{{% /badge %}} Linking of Health Records (HIP_INTI_LINK_305)|HIP system links the ABHA Number / Address with the patient records|1. Link Health Records. 2. Through PHR Application| check if the linked records can be pulled
4.1|HIP Initiated Health Record Linking Using Direct Auth|{{% badge style="blue" %}}Mandatory for the Govt. Integartors{{% /badge %}} Direct Auth mode for Linking of Health Records (HIP_INTI_LINK_401)|The system should have provision to link patient's Health record with ABHA address |1. Enter patient's ABHA address on the System. 2. The user logs into their PHR Application| receives the request for approval and approves it. 3. Search the request in the Notification tab. 4. Approve the request.(User may approve or reject the request. if the request is rejected process ends there). 5. Upon successful validation of OTP| linking token is generated.
4.2|HIP Initiated Health Record Linking Using Direct Auth|{{% badge style="blue" %}}Mandatory{{% /badge %}} Linking of Health Records (HIP_INTI_LINK_404)|HIP system links the ABHA Address with the patient records|1. Link Health Records. 2. Through PHR Application| check if the linked records can be pulled.
5.1|HIP Initiated Health Record Linking Using Demographic Auth|{{% badge style="blue" %}}Mandatory for the Govt. Integartors  {{% /badge %}} Link record via Demographic Auth (HIP_INTI_LINK_501)|The system should have provision to link patient's Health record with ABHA address.|1. for the verified ABHA Address of the patient in the HIP System. 2.The user provides their demographic details (name, gender, DOB, mobile number). 3. Enter user/patient's demographic details in the HIP System
5.2|HIP Initiated Health Record Linking Using Demographic Auth|{{% badge style="blue" %}}Mandatory{{% /badge %}} Validate the demographic details  (HIP_INTI_LINK_503)|The HIP validates demographic details of patient|1. Validate Demographic Details ( Provided by the user and fetch by the ABHA address). 2.Upon successful validation of OTP| linking token is generated.
5.3|HIP Initiated Health Record Linking Using Demographic Auth|{{% badge style="blue" %}}Mandatory{{% /badge %}} Linking of Health Records (HIP_INTI_LINK_505)|HIP system links the ABHA Address with the patient records|1. Link Health Records. 2. Through PHR Application| check if the linked records can be pulled"


## Test Cases for PHR Applicationlication

S.No|Function|Functionality|Test Case|Steps To Be Executed 
|--|----|------|-----|-----|
1.1|User Initiated Health Record Linking|{{% badge style="blue" %}}Mandatory{{% /badge %}} Search for Facility/ HIP (USER_INIT_LINK_602)|1. Patient logs in PHR Application. 2. PHR Application must provide an option to search health providers (provider can be hospitals, labs, clinics, nursing home, doctor, govt Health program, telemedicine provider|1. Search for required HIP. 2. Select that HIP
1.2|User Initiated Health Record Linking|{{% badge style="blue" %}}Mandatory{{% /badge %}} Share User Profile Details with Facility/ HIP (USER_INIT_LINK_603)|PHR Application must share user's profile details (Mobile no., ABHA Number, ABHA Address, Name, Gender, Year of Birth and Patient ID (optional) with the Facility/HIP.| Profile Details will be  shared.
1.3|User Initiated Health Record Linking|{{% badge style="blue" %}}Mandatory{{% /badge %}} Fetch Health Records (USER_INIT_LINK_604)|PHR Application must fetch/ receive Health Records available with the selected HIP/ Facility for the shared profile details.|Receive list of Health Records that are available with the Facility/ HIP
1.4|User Initiated Health Record Linking|{{% badge style="blue" %}}Mandatory{{% /badge %}} Provide Consent for Health Record Linking (USER_INIT_LINK_605)|PHR Application will prompt to enter an OTP received on the user's mobile number.|1. Select "Link Health Records" on PHR Applicationlication. 2. Receive OTP on mobile number. 3. Enter OTP and provide consent for health record linking.
1.5|User Initiated Health Record Linking|{{% badge style="blue" %}}Mandatory{{% /badge %}} Pull Records (USER_INIT_LINK_607)|In PHR Application user will able to pull the records.|Through PHR Applicationlication,check if the linked records can be pulled
2.1|SHARE PROFILE|{{% badge style="blue" %}}Mandatory{{% /badge %}} Share Patient Profile (SHARE _PATIENT_PROFILE_701)|User will scan the QR code which is placed the facility premises.|1. Log into PHR Application. 2. User will scan the QR code which is placed the facility premises. 3. Post scanning, patient profile details are displayed including ABHA number, ABHA address, Name, Gender, DoB, Mobile No and Address. Below this consent language is displayed - "You consent to the above information to be shared with (HIP Name). They can use this information for your registration and linking your health records" and both "Cancel" / "Share" buttons are provided. 4.Check that after clicking on "Share" button, user profile is successfully shared with the HIP and if user click on "Cancel" button then user profile is not shared with the HIP. 5. User clicks on share and gets a token number. 6. User clicks on ok and gets token number with validity of 30 minutes.