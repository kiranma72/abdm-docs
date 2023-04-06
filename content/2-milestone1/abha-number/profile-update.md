+++
title = "Profile Update"
date = 2023-04-05T01:30:25+05:30
weight = 6
chapter = true
pre = "<b>2.1.6 </b>"
+++


# Profile Update

|  Applicable To                             |   HMIS / LMIS (PVT)  |   Government Health App  |     
|-------------------------------|:----------------------:|:--------------------:|
|   Using Aadhar Demographic                      |  {{% badge %}}Optional{{% /badge %}}       |  {{% badge %}} Optional{{% /badge %}}        |  



- If you want to do profile update for any user, you can do it by using their ABHA number, via:
	1. [**ABHA Website**](https://abha.abdm.gov.in/), if you ABHA number was created on Production website.
	2. [**ABHA Sandbox**](https://sandbox.abdm.gov.in//), if you ABHA number was created on Sandbox environment.

- If you want to do it in your application,  more information is documented under PHR Application section

## Test Cases

Functionality|Test Case|Steps To Be Executed|
| ----- | ----- | ----- |
{{% badge %}}Optional{{% /badge %}} Mobile Update (PROF_ABHA_601)|System must allow the user to update their Mobile number|1. Enter new mobile number. 2. Enter OTP. 3. Enter Password/ OTP on old mobile number.|
{{% badge %}}Optional{{% /badge %}} Photo Update (PROF_ABHA_602)|System must allow the user to update their Photo|1. Click on Edit Photo. 2. Upload new photo|
{{% badge %}}Optional{{% /badge %}} Email Update (PROF_ABHA_603)|System must allow the user to update their Email|1. Enter new Email ID. 2. Enter OTP|
{{% badge %}}Optional{{% /badge %}} Re-KYC (PROF_ABHA_604)|System must allow the user to perform re-KYC|1. Click on re-KYC option. 2. Enter OTP received on Aadhaar linked mobile number|
{{% badge %}}Optional{{% /badge %}} Delete ABHA (PROF_ABHA_605)|System must allow the user to Delete/ Deactivate ABHA|1. Click on Delete/ Deactivate ABHA. 2. Enter OTP received on mobile number to confirm deletion/ deactivation. 3. Try to login again using the same ABHA|