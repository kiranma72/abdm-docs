+++
title = "Discovery & Linking Records"
date = 2023-05-02T03:53:25+05:30
weight = 7
chapter = true
pre = "<b>5.7 </b>"
+++

# Discovery and Linking of Records

## Functionality Overview



## Test Cases

**Health and Facility records linking: User initiated linking flow (Discovery Flow) - Complete Discovery of HIP, linking, fetching and viewing of records in PHR app** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Link HIP|After Login : Click on "Link my Health Records" tab in "My Records" tab|Click on "Link my Health Records" tab / "+" symbol in "Linked Facility" tab to search records in HIP
2.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Discover HIP|Search HIP 's such as hospital, clinic, lab to discover them based on typed string by the individual|When individual will search the visited facilty (HIP), the entire facilty name with complete address will be discovered by the individual. This "Search" is based on string, i.e HIP name entered by the patient in the search bar of PHR app.
3.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Display of patient details	| After searching facility: The details visible to patient on the PHR app are: Verified mobile number, ABHA address, ABHA number, Patient ID, Full Name, Year of Birth, Gender. | Details of Patient will be visible when individual search for the HIP in PHR app while user initiated linking flow.
4.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Fill Patient ID (Optional)	| This customizable lable is: Patient ID - In case of linking health records created at health facility. And this field is optional for patient to enter. | Check, if exact match of record is found after entering correct Patient ID 
5. | {{% badge style="blue"  %}}Mandatory{{% /badge %}}  Matching of API specifications to link record | Click on "Fetch Records". After matching following fields, records will be fetched from facility (HIP) to PHR app: Name (Mandatory), Year of Birth (Mandatory), Gender (Mandatory), Mobile Number (Mandatory), Patient ID (Optional) | Ensure that already linked care context should not be discovered in PHR mobile app. If all care context of discovered facilty are already linked, then display message called "All your existing records are linked. No additional records availaible for linking". Ensure that the linked care context is shown in the "Linked Facility" tab of the PHR mobile app
6.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Link records|Display of records details like HI type | Display of all correct details of records, after matching of API specifications. Select the record which patient wants to link and click on "Link Selected"
7.|{{% badge %}}Optional{{% /badge %}}  Fill mobile OTP received to complete linking of record. | Mobile OTP will be received once individual clicks on fetch records. After successful validation of OTP, display message called “Records are successfully linked”. This OTP is sent by HIP to the patient's mobile. | Fill mobile OTP for successful linking of facility. Error message display, for following scenarios : **Scenario 1:** If there is Communication Gap, between HIP and individual – Due to some technical issue at HIP end like if server is down then, error message is displayed as “Couldn’t Connect: We are sorry. Unable to contact your hospital. Please try again later”. **Scenario 2:** If individual have never visited the hospital – An error message is displayed as “No health records found”. **Scenario 3:** Records of all visits are already linked and there is nothing new to link - – An error message is displayed as “No new health record to link: Records of all visits are already linked and there is nothing new to link
8.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Linked facility will be visible in "Linked Facility" tab. Click on "Pull Records" button to fetch and view records.| Ensure that the patient's health-records are getting fetched. | 1. Check that PHR app sends data transfer request to HIP within 5 minutes after an individual click on "Pull Records" button. 2. Ensure that the patient health records are fetched within 2 hours in the PHR mobile app. Ensure that the patient's health-records are fetched without ERRORED"
9.|{{% badge %}}Optional{{% /badge %}}  Display message regarding fetching of records may take time in "My Records" tab | 1. Keep "I" button in "My Records", so that message is displayed regarding fetching of records may take time when patient hovers over i button. 2. Check that proper error or status message will be displayed if records are taking time in fetching. For e.g. Refresh to fetch record, Data fetch in progress etc..|Since, fetching of records take time. Display message called "Recently linked records might take some time to show" when patient hover over "i button" in "My Records" tab.
10. | {{% badge %}}Optional{{% /badge %}} Records will be displayed in "My Records" tab. | Click on the attached report to view the health record. | After clicking on record: Details of health record will be displayed alongwith an attachment consisting of record. Details of health record included structured data such as: Facility Name, Visit type, Prescribed By, Date and Time
11.| {{% badge %}}Optional{{% /badge %}} View record in mobile device |	Record will open when individual clicks on the attachment consisting health record | Records will open in the device and patient can view it

**Health Programme records linking, fetching and viewing of records: User initiated linking (Discovery Flow)** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Link Programme	| After Login : Click on "Link my Health Records" tab in "My Records" section|Click on "Link my Health Records" tab / "+" symbol in "Linked Facility" tab to search records in HIP.
2.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Select Health Programme|Select programme name whose record patient wants to link, fetch and view in PHR app. Currently, government health programmes such as "CoWIN", "AB-PMJAY", e-Sanjeevani OPD, e-Sanjeevani HWC, RCH programme. Going forward, other health programmes will also integrate with PHR app"	| Check, if patient is able to select the integrated government health programme with the PHR app.
3. | {{% badge style="blue"  %}}Mandatory{{% /badge %}}  Display of patient details	| After clicking on programme name, the details visible to patient are: Verified mobile number, ABHA address, ABHA number, CoWIN registered mobile no (Customizable Label - Optional), Full Name, Year of Birth, Gender	| In User initiated linking (Discovery Flow), details of patient will be visible when individual select government health programme in PHR app.
4. | {{% badge style="blue"  %}}Mandatory{{% /badge %}}  Fill PM-JAY ID (Optional) | This customizable label is: 1. PMJAY ID - In case of linking health records from AB-PMJAY programme. 2. CoWIN Registered Mobile No - In case of linking health records from CoWIN. | Check, if exact match of patient records are found, after entering correct PMJAY ID / CoWIN registered mobile number
5. | {{% badge style="blue"  %}}Mandatory{{% /badge %}}  Matching of API specifications | "Click on "Fetch Records". After matching following fields, records will be fetched from programme to PHR mobile app: Name (Mandatory), Year of Birth (Mandatory), Gender (Mandatory), Mobile Number (Mandatory), Patient ID (Optional)	| Ensure that already linked care context should not be discovered in PHR mobile app. If all care context of selected government health programme are already linked, then display message called "All your existing records are linked. No additional records availaible for linking". Ensure that the linked care context is shown in the "Linked Facility" tab of the PHR mobile app
6.| {{% badge style="blue"  %}}Mandatory{{% /badge %}}  Link records	| Display of records details such as Dose 1, Dose 2 and Dose 3 (Precautionary dose) in case of CoWIN programme. | Display of all correct details of records, after matching of API specifications
7.| {{% badge style="blue"  %}}Mandatory{{% /badge %}} 	Display of records details such as Dose 1, Dose 2 and Dose 3 (Precautionary dose) in case of CoWIN programme. | Select the record which patient wants to link and click on "Link Selected"
8. | {{% badge %}}Optional{{% /badge %}} Fill mobile OTP received to complete linking of record. | Mobile OTP will be received once individual clicks on fetch records. After successful validation of OTP, display message called “Records are successfully linked”. This OTP is sent by government health programme to the patient's mobile. | Fill mobile OTP for successful linking of facility.
9.|{{% badge %}}Optional{{% /badge %}} Fill mobile OTP received to complete linking of record. | Mobile OTP will be received once individual clicks on fetch records. After successful validation of OTP, display message called “Records are successfully linked”. This OTP is sent by government health programme to the patient's mobile. | Fill mobile OTP for successful linking of facility 
10.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Linked programme will be visible in "Linked Facility" tab. Click on "Pull Records" button to fetch and view records|Ensure that the patient's health-records are getting fetched|1. Check that PHR app sends data transfer request to HIP within 5 minutes after an individual click on "Pull Records" button. 2. Ensure that the patient health records are fetched within 2 hours in the PHR mobile app
11.|{{% badge style="blue"  %}}Mandatory{{% /badge %}}  Linked programme will be visible in "Linked Facility" tab. Click on "Pull Records" button to fetch and view records|Ensure that the patient's health-records are getting fetched|Ensure that the patient's health-records are fetched without ERRORED
12.|{{% badge %}}Optional{{% /badge %}}  Display message regarding fetching of records may take time in "My Records" tab. |1. Keep "I" button in "My Records", so that message is displayed regarding fetching of records may take time when patient hovers over i button. 2. Check that proper error or status message will be displayed if records are taking time in fetching. For e.g. Refresh to fetch record, Data fetch in progress etc. | Since, fetching of records take time. Display message called "Recently linked records might take some time to show" when patient hover over "i button" in "My Records" tab.
13. | {{% badge %}}Optional{{% /badge %}} Records will be displayed in "My Records" tab. Click on the attached report to view the health record.|After clicking on record: Details of health record will be displayed alongwith an attachment consisting of record	| Details of health record included structured data such as: Facility Name, Visit type, Prescribed By, Date and Time
14. | {{% badge %}}Optional{{% /badge %}} View record in mobile device |	Record will open when individual clicks on the attachment consisting health record|Records will open in the device and patient can view it


## API Sequence Diagram


## API Collection

