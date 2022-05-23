---
title: "Sign Up or Sign in using PHR Addr"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---

# Sign up or Sign in using PHR Address
# Sign up/Registration in PHR App
The PHR application developed by ABDM is now known as ABHA mobile application and has been taken as an reference PHR application. In this application, by registration we means creating ABHA address aka PHR address, which is an easy to remember PHR address along with its password to login. 
In the ABHA app which is an reference app, registration can be done by two ways:
1. Self declared registration (Mobile or Email)
2. KYC Verified registration (Aadhar/DL/PAN)
## Registration via ABHA Number (KYC-Verified)
For registering using ABHA number, individual has to choose the option of ABHA number and enter the 14-digit ABHA number. Once entered individual will autheticate ABHA number either via Aadhar OTP or Mobile OTP. 
After validating the OTP, the individual's profile details are auto populated from ABHA system. Already linked ABHA addresses will be displayed along with the option of creating New ABHA address. Individual can either choose already linked ABHA addresses to login or can create new ABHA address.
For creating new ABHA address, inidvidual can choose an ABHA address from the suggestions displayed based on the user profile details or can create a different ABHA address as per ABHA Address creation policy, along with password. New ABHA address will be created for the given ABHA number and user can directly login.
![alt text](Picture 1.png) ![alt text](Picture 2.png) ![alt text](Picture 3.jpg) ![alt text](Picture 4.png) ![alt text](Picture 5.png)
**APIs for registering using ABHA number**
1. **/v1/apps/registration/hid/confirm-init**
Explanation - Api Checks Health ID Number to find User.
Request Body - Required
Response - Retrun session in case of success against request.

```
{
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "value": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI="
}
```
### Registration via Mobile Number
For registering using Mobile number, Individual has to choose the option of Mobile number and enter the Mobile number. Once entered individual will autheticate MObile number via OTP.  
After validating the OTP, list of already linked ABHA addresses will be displayed along with the option of creating New ABHA address. 
Individual can either choose already linked ABHA addresses to login or can create new ABHA address by selecting “Still want to create a new ABHA address?” When individual selects “Still want to create new ABHA address?” he/she can fill all the demographic details like
1.	Full name (Mandatory)
2.	Date of Birth (Year- Mandatory)
3.	Gender (Mandatory)
4.	Email ID (Optional)
5.	Address (Mandatory)
6.	State (Mandatory)
7.	District (Mandatory)
8.	Pin Code (Mandatory)
For creating new ABHA address, inidvidual can choose an ABHA address from the suggestions displayed based on the user profile details or can create a different ABHA address as per ABHA Address creation policy, along with password. New ABHA address will be created for the given ABHA number and user can directly login.
#### Registration via Email ID
For registering using Email ID, Individual has to choose the option of Email ID and enter the Email ID. Once entered individual will autheticate Email ID via OTP.  
After validating the OTP, list of already linked ABHA addresses will be displayed along with the option of creating New ABHA address. 
Individual can either choose already linked ABHA addresses to login or can create new ABHA address by selecting “Still want to create a new ABHA address?” When individual selects “Still want to create new ABHA address?” he/she can fill all the demographic details like
1.	Full name (Mandatory)
2.	Mobile number (Optional)
3.	Date of Birth (Year- Mandatory)
4.	Gender (Mandatory)
5.	Address (Mandatory)
6.	State ((Mandatory)
7.	District (Mandatory)
8.	Pin Code (Mandatory)
For creating new ABHA address, inidvidual can choose an ABHA address from the suggestions displayed based on the user profile details or can create a different ABHA address as per ABHA Address creation policy, along with password. New ABHA address will be created for the given ABHA number and user can directly login.

