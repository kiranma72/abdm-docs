+++
title = "Link and Unlink"
date = 2023-05-02T03:53:25+05:30
weight = 14
chapter = true
pre = "<b>5.14 </b>"
+++

# Link/Unlink PHR Address to an ABHA number

## Functionality Overview



## Test Cases

**Link/Unlink ABHA no to the ABHA address** 

S.No|Functionality|Test Case|Steps To Be Executed 
|--|------|-----|-----|
1| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Link ABHA no to the ABHA address|Click on "Link ABHA Number" option provided beside "Self Declared" in home screen 
2| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Link ABHA no to the ABHA address|Enter 14-digit ABHA no 
3| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Link ABHA no to the ABHA address|Validate ABHA no via aadhar OTP / mobile OTP|Check that an individual is able to validate ABHA no via both aadhar OTP / mobile OTP
4| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Link ABHA no to the ABHA address|Resend OTP| if OTP is not received in 60 seconds|Check that resend OTP option is provided after 60 seconds for both aadhar OTP / mobile OTP
5| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Link ABHA no to the ABHA address|Displaye message: "Congratulations! Your ABHA number is now linked to your existing ABHA address. ABHA number is visible on your profile.|Check that post OTP validation of ABHA no| message is displayed that ABHA no is successfully linked with the ABHA address and ABHA number is visible in profile. Also| ABHA number policy will supersede ABHA address. Hence| profile details will change as per ABHA number. In addition to this| "Self-Declared" status is changed to "KYC Verified" in home screen.
6| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Link ABHA no to the ABHA address|Click on "Go back to home screen" tab to go back to profile|Check that after clicking on "Go back to home screen" tab| an individual is able to go back to home screen
7| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Unlink ABHA no to the ABHA address|Click on "Unlink ABHA Number" option provided beside 14-digit ABHA number in home screen. 
8| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Unlink ABHA no to the ABHA address|Display confirmation message: "Even after unlinking ABHA number| you will still be able to share your health records with healthcare providers through ABHA address. Do you still want to unlink ABHA number XX-XXXX-XXXX-XXXX with your existing ABHA address?" (Yes/No)          |Ckeck that confirmation message is displayed before unlinking ABHA no with ABHA address
9| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Unlink ABHA no to the ABHA address|Validate ABHA no by selecting any one of the option - "OTP is sent on mobile number linked with your aadhar" / "OTP on mobile number linked with your ABHA number|Check that an individual is able to validate ABHA no via OTP received on mobile no linked with aadhar / ABHA no
10| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Unlink ABHA no to the ABHA address|Resend OTP| if OTP is not received in 60 seconds|Check that resend OTP option is provided after 60 seconds for both mobile no linked with aadhar / ABHA no
11| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Unlink ABHA no to the ABHA address|Display message: "ABHA number is unlinked to existing ABHA address. Now| ABHA number is not visible in your profile|Check that post OTP validation of ABHA no| message is displayed that ABHA no is successfully unlinked with the ABHA address and ABHA number is not visible in profile.
12| {{% badge style="blue" %}}Mandatory{{% /badge %}}  Unlink ABHA no to the ABHA address|Click on "Go back to home screen" tab to go back to profile|Check that after clicking on "Go back to home screen" tab| an individual is able to go back to home screen


## API Sequence Diagram


## API Collection

