+++
title = "Sharing PHR address"
date = 2023-05-02T03:53:25+05:30
weight = 13
chapter = true
pre = "<b>5.13 </b>"
+++

# Sharing your PHR address at a Health facility

## Functionality Overview



## Test Cases

**Scan and Share** - Scan the QR code to share information.

Scan QR Code at the ABDM compliant health facility to get token number for better queue management and completing faster patient registration.

There are 2 use-cases here:
**1. Use-case 1: Patients can scan the Health Facility QR Code using any PHR application**

S.No|Functionality|Test Scenario|Steps To Be Executed 
|--|------|-----|-----|
1.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using PHR App | Use-case 1 - Patient can scan the QR Code using any PHR app such as ABHA mobile app|Check that, patient is able to login to any PHR app such as ABHA mobile app. 
2.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using PHR App | Use-case 1 - Patient can scan the QR Code using any PHR app such as ABHA mobile app|Check that patient is able to click on "QR Code icon" and scan the QR Code at ABDM compliant health facility.
3.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using PHR App | Use-case 1 - Patient can scan the QR Code using any PHR app such as ABHA mobile app|Check that, post clicking on share button, patient profile details are successfully shared to the HMIS side with consent of the patient.
4.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using PHR App | Use-case 1 - Patient can scan the QR Code using any PHR app such as ABHA mobile app|Check thatnotification is displayed for patient to know that profile details are successfully shared with the hospital and token number is also displayed. 
5.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using PHR App | Use-case 1 - Patient can scan the QR Code using any PHR app such as ABHA mobile app|Check that post click on "OK" button, token number is displayed and it is valid for next 30 minutes. This time duration is configurable. 

**2. Use-Case 2: Scan the QR Code through third party scanner / phone camera**

S.No|Functionality|Test Scenario|Steps To Be Executed 
|--|------|-----|-----|
1.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile and patient is already logged on in the PHR app | Check that, QR Code is scanned using phone camera or any 3rd party QR scanner
2.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile and patient is already logged on in the PHR app |Check that installed ABDM Compliant PHR apps and browser is displayed. Patient can click on chrome browser to open the user initiated deep link web page to see the complete listing of ABDM compliant PHR apps.
3.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile and patient is already logged on in the PHR app |Check that post clicking on any one of the PHR apps, patient is redirected to share profile page of PHR app as patient is logged-in  to the PHR app
4.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile and patient is already logged on in the PHR app |Check that post clicking on share button, patient profile details are successfully shared to the HMIS side with consent of the patient.
5.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile and patient is already logged on in the PHR app |Check that notification is displayed, that the profile details are shared with the hospital and token number is also displayed. 
6.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile and patient is already logged on in the PHR app |Check that post click on "OK" button, token number is displayed and it is valid for next 30 minutes. This time duration is configurable. 
7.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile but patient is not logged on in the PHR app | Check QR Code can be scanned using phone camera or any 3rd party QR scanner.
8.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile but patient is not logged on in the PHR app | Check that installed ABDM Compliant PHR apps and browser is displayed. Patient can click on chrome browser to open the user initiated deep link web page to see the complete listing of ABDM compliant PHR apps.
9.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile but patient is not logged on in the PHR app | Post clicking on any one of the PHR apps, patient is redirected to login page of PHR app as patient is not logged-in  to the PHR app 
10.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile but patient is not logged on in the PHR app |Check that post successful login, patient is redirected to share profile page of PHR app.
11.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile but patient is not logged on in the PHR app |Check that post clicking on share button, patient profile details are successfully shared to the HMIS side with consent of the patient.
12.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile but patient is not logged on in the PHR app |Check that notification is displayed, that the profile details are shared with the hospital and token number is also displayed. 
13.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | ABDM compliant PHR application is already installed in patient's mobile but patient is not logged on in the PHR app |Check that post click on "OK" button, token number is displayed and it is valid for next 30 minutes. This time duration is configurable. 
14.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | No ABDM compliant PHR application is installed in patient's mobile device. |Check that QR Code can be scanned using phone camera or any 3rd party QR scanner 
15.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | No ABDM compliant PHR application is installed in patient's mobile device. |Check that User Initiated Deep Link Web Page opens, and patient can see the complete listing of ABDM compliant PHR apps.
16.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | No ABDM compliant PHR application is installed in patient's mobile device. |Check that once patient selects any one of the PHR app, he/she is redirected to Google Play Store / app store to download / install the selected mobile PHR app
17.|{{% badge style="blue" %}}Mandatory{{% /badge %}} Scan Health QR Code using 3rd party camera | No ABDM compliant PHR application is installed in patient's mobile device. |Check that, selected PHR app is launched after installation and patient will create ABHA address and password



## API Sequence Diagram


## API Collection

