+++
title = "Using ABHA Number"
date = 2023-03-16T09:30:25+05:30
weight = 4
chapter = true
pre = "<b>4.2.2 </b>"
+++

# Using ABHA Number
|  Applicable To                             |   HMIS / LMIS (PVT)  |   Government Health App  |   PHR / LOCKER    |
|-------------------------------|:----------------------:|:--------------------:|:-------------------:|
|   Using ABHA Number                     |  {{% badge %}}Optional{{% /badge %}}       |  {{% badge %}}Optional{{% /badge %}}         |  {{% badge style="blue"%}} Mandatory{{% /badge %}}       |

## Functionality Overview

**Description:** Individual enters ABHA address (xyz@abdm), and it is validated depending on auth mode of validation such as mobile OTP/aadhar OTP/email OTP or Password to Login.

 - In this flow Individual is given an option of creating ‘ABHA address through ABHA (Number) via KYC document. Please note, the list of KYC documents may be revised from time to time.
 - Create an ABHA address of the format abc@abdm via 14-digit ABHA (Number). In this case, profile details like photo, name, date of birth, gender, mobile no, email ID, and address are fetched from the ABHA system.
 - Individual creates an easy to remember ABHA Address along with its password to login
   - Individuals may link/unlink ABHA (Number) with ABHA address as per their choice.


**ABHA Address Policy**

1. ABHA Address Policy:
	- Minimum length 4 including alphabet, number & dot(.) are allowed. Number cannot be in beginning and dot(.) cannot be in beginning & end.
	- As a policy we allow creation of all numeric Abha addresses for Abha Number only: 14digit@abdm.

2. 10-digit Mobile number as ABHA Address:
	- For now, we have restricted the creation of (10 digit) Mobile.No@ABDM

3. Creation of (14 digit@abdm):
	- ABHA Address is not allowed however we have the provision for the user to login with same 14digit@abdm both in web PHR and mobile PHR.

4. Password validation :
	- This has been made optional. You may kindly check the below APIs at your end and reach out to us in case of any issues:
		- Registration via ABHA:/api/v1/phr/registration/hid/create-phr-address
		- Registration via Mobile and Email: /api/v1/phr/registration/create/phr

## Test Cases

*check with Kiran*

Functionality|Test Case|Steps To Be Executed|
| ----- | ----- | ----- |
{{% badge style="blue" %}}Mandatory{{% /badge %}} add |add |add


## API Sequnce Diagram

*check with Kiran*

## API Informaion

*check with Kiran*

