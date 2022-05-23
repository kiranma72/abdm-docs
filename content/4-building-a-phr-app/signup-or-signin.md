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

<img width="184" alt="Picture1" src="https://user-images.githubusercontent.com/105836429/169759881-3f40a1c9-d442-4a63-beec-eaae5ad7f4ab.png">
<img width="184" alt="Picture2" src="https://user-images.githubusercontent.com/105836429/169759890-cb9fce56-f1e3-454a-bba4-553718d0e3f7.png">
<img width="184" alt="Picture3" src="https://user-images.githubusercontent.com/105836429/169759894-63a71fe4-74c4-431a-98a1-fc842fadf9fe.jpg">
<img width="184" alt="Picture4" src="https://user-images.githubusercontent.com/105836429/169759898-50a3cf78-ce1c-42ee-b5de-707a43c2f14e.png">
<img width="184" alt="Picture5" src="https://user-images.githubusercontent.com/105836429/169759900-67a02408-25a1-432f-8f8f-47ea9499a66d.png">

**APIs for registering using ABHA number**
1. **/v1/apps/registration/hid/confirm-init**
Explanation - Api Checks Health ID Number to find User.
Request Body - Required
Response - Retrun session in case of success against request.

Parameters 

No Parameters

Request body (In application/JSON)

**Example for request body**
```
{
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "value": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI="
}
```
Responses

Return status as true alone with partail details of Health id number in case of success

**Example for Response**
```
{
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "name": {
    "firstName": "Shubhanshu",
    "middleName": "Kumar",
    "lastName": "Shukla"
  },
  "gender": "Male",
  "dateOfBirth": {
    "date": 14,
    "month": 1,
    "year": 1996
  },
  "healthIdNumber": "43-4221-5105-6749",
  "stateName": "MAHARASHTRA",
  "stateCode": "27",
  "districtCode": "401",
  "districtName": "Pune",
  "pincode": "412306",
  "aadhaarVerified": true,
  "profilePhoto": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkJCQkJCQoLCwoODw0PDhQSERESFB4WFxYXFh4uHSEdHSEdLikxKCUoMSlJOTMzOUlUR0NHVGZbW2aBeoGoqOIBCQkJCQkJCgsLCg4PDQ8OFBIRERIUHhYXFhcWHi4dIR0dIR0uKTEoJSgxKUk5MzM5SVRHQ0dUZltbZoF6gaio4v/CABEIBLAHgAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwABBAUGB//aAAgBAQAAAADwawLpMspcK7qrlE5F0Vtul2bVywMUNeBHUkW/bmxvYELGuNjh2VDvixxo5ViljKjDRMoahCULjs2JCShjhjh2OGxo0Y2MoXHOLszsKLhw7tD99mpZQxj8xceofmLEKFwXLTIyHwY1Ls+iEotjHY0M0pjRYxtGj4VFKLPohQlFQyy4Qipc0XG9pS+CP/2Q==",
  "authMethods": "AADHAAR_OTP",
  "email": "example@demo.com",
  "mobile": "9545812125",
  "kycPhoto": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI=",
  "phrAddress": [
    "string"
  ],
  "tags": {
    "additionalProp1": "string",
    "additionalProp2": "string",
    "additionalProp3": "string"
  }
}
```

2. **/v1/apps/create/registration/hid/create/phrAddress**

Parameters 

No Parameters

Request body (In application/JSON)

**Example for request body**
```
{
  "alreadyExistedPHR": true,
  "password": "HNceo964MVndrs8Z2oMtzIsmmbzagveHbWkDsDKskTue+/YZhHHrMon19J03ggU457upzWMIX0nU3d38xjB3FxA2qWCVmvLZ98A9l0y3i33vq1ywu9cORGF4OEqV8l7H9h4tDnLGDHnbOh9ct85VfOohP4p73lqW6WQSMYcU+xkBfEsRj42pWL19EVsE1UULtQE8gYY1B0SeM63svUp1kQ4Pt5hdgKxibYBq+hRcck2PkEIhp2N7AkjH4Tf+AhXU9956WLwjKgAKMk7K4+Zv8JtxYCcblQitbpN4ImPH5edf4mO5R/L9RpdAVSllAQQfPIDlp5ZGOZ1GrSmhzOSP3g==",
  "phrAddress": "user@abdm",
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```
Responses

OK

**Example for Response**
```
{
  "phrAdress": "user@abdm",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
}
```

3. **/v1/apps/registration/hid/auth-init**

Explanation - Api Checks Health ID Number to find User.
Request Body - Required
Response - Retrun transaction in case of success against request.

Parameters 

No Parameters

Request body (In application/JSON)

**Example for request body**
```
{
  "healthIdNumber": "22-2626-4321-7532",
  "purpose": "CM_ACCESS",
  "authMode": "MOBILE_OTP",
  "requester": {
    "type": "PHR",
    "id": "IN0400XX"
  }
}
```
Responses
Return status as true alone with partail details of Health id number in case of success
**Example for Response**
```
{
  "sessionId": "31216fed-4a23-4a18-ac89-03c9f3a0bf89"
}
```

4. **/v1/apps/registration/hid/search/auth-mode**
Explanation - Api Checks Health ID Number to find User.
Request Body - Required
Response - Retrun partial details of Health ID Number.

Parameters 

No Parameters

Request body (In application/JSON)

**Example for request body**
```
{
  "healhtIdNumber": "11-1111-1111-1111"
}
```
Responses
Return status as true alone with partail details of Health id number in case of success
**Example for Response**
```
{
  "authMethods": [
    "string"
  ],
  "blockedAuthMethods": [
    "string"
  ],
  "healthIdNumber": "string",
  "status": "string"
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

<img width="184" alt="Picture6" src="https://user-images.githubusercontent.com/105836429/169763808-1b2ec097-7e28-4b71-a68b-c98600ed5a0a.png">
<img width="184" alt="Picture7" src="https://user-images.githubusercontent.com/105836429/169763818-ca8338c2-d02e-40b3-bab3-4f8f3bbae764.jpg">
<img width="184" alt="Picture8" src="https://user-images.githubusercontent.com/105836429/169763823-7d033d5e-3a9f-4a6f-b467-a860a19dc5e9.jpg">
<img width="184" alt="Picture9" src="https://user-images.githubusercontent.com/105836429/169764605-f5521dbd-d1c6-4205-b8ed-4cb4552f9a3b.png">
<img width="184" alt="Picture10"src="https://user-images.githubusercontent.com/105836429/169765445-617a9190-3d0e-4d6d-97f0-4a3539e2a326.png">

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

<img width="184" alt="Picture11"src="https://user-images.githubusercontent.com/105836429/169766759-ef6210e7-6e42-4c80-870e-f46af9d3cd34.png">
<img width="184" alt="Picture12"src="https://user-images.githubusercontent.com/105836429/169766767-81865de8-30e7-48e1-93ed-7e99edc0d314.png">
<img width="184" alt="Picture13"src="https://user-images.githubusercontent.com/105836429/169766773-66abe7d9-420d-4a51-a2e9-acfafea1a8c1.jpg">
<img width="184" alt="Picture14"src="https://user-images.githubusercontent.com/105836429/169766778-ba5e4050-051a-495a-8743-de6170fab1f9.png">
<img width="184" alt="Picture15"src="https://user-images.githubusercontent.com/105836429/169766803-7ec3513b-6897-4381-9d35-bf2fcaffde6d.png">

**APIs for registering using Mobile number or Email ID**
1. **/v1/apps/create/phrAddress**
To Register the beneficiary.
Beneficiary data required to pass in the request
Request
Below is the Request Parameters description

Attributes	Description
sessionId * required	Session Id, Based on UUID.
phrAddress * required	PHR address of the Beneficiary or user
password * required	Password for the account. Same will be used to login to PHR Account. Password must contain an uppercase, a lowercase, a number, a special character (@,_$,#) and at least 8 or more characters. It should not contain any sequences (like 123)
Note :

1. Password must be in encrypted form, Plain text form Password is not allowed in request
Parameters 

No Parameters

Request body (In application/JSON)

**Example for Request body**
```
{
  "alreadyExistedPHR": true,
  "password": "HNceo964MVndrs8Z2oMtzIsmmbzagveHbWkDsDKskTue+/YZhHHrMon19J03ggU457upzWMIX0nU3d38xjB3FxA2qWCVmvLZ98A9l0y3i33vq1ywu9cORGF4OEqV8l7H9h4tDnLGDHnbOh9ct85VfOohP4p73lqW6WQSMYcU+xkBfEsRj42pWL19EVsE1UULtQE8gYY1B0SeM63svUp1kQ4Pt5hdgKxibYBq+hRcck2PkEIhp2N7AkjH4Tf+AhXU9956WLwjKgAKMk7K4+Zv8JtxYCcblQitbpN4ImPH5edf4mO5R/L9RpdAVSllAQQfPIDlp5ZGOZ1GrSmhzOSP3g==",
  "phrAddress": "user@abdm",
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```
Responses
Return user token id in case of success
**Example for Responses**
```
{
  "phrAdress": "user@abdm",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
}
```

2. **/v1/apps/registration/details**
To Register the beneficiary.
Beneficiary data required to pass in the request
Request
Below is the Request Parameters description

Attributes	Description
sessionId * required	Transaction number, Based on UUID.
first * required	First Name of the Beneficiary mentioned in the documents
middle	Middle Name of the Beneficiary mentioned in the documents
last	Last Name of the Beneficiary mentioned in the documents
gender * required	Male - M, Female - M, Other - O
email * required	Valid E-mail address of the beneficiary (Encrypted)
mobile* required	Valid 10-digit Mobile Number(Note - Mobile number must be encrypted) of the Beneficiary(Encrypted).
dayOfBirth * required	day of birth
monthOfBirth * required	month of birth
yearOfBirth * required	year of birth
stateCode * required	Valid State Code (LGD)
districtCode	Valid District Code (LGD).
countryCode	Country code.
pincode * required	Pincode
address	Valid Address as per documents.
Parameters 

No Parameters

Request body (In application/JSON)

**Example for Request body**
```
{
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "name": {
    "first": "Shubhanshu",
    "middle": "Kumar",
    "last": "Shukla"
  },
  "dateOfBirth": {
    "date": 14,
    "month": 1,
    "year": 1996
  },
  "gender": "M",
  "stateCode": "7",
  "districtCode": "77",
  "email": "6BE4FfCtkOrDZU/Fc545GrhVGgC8JxiK8uU/DSQT7PNebX2Bigz0lUuC3R0F4RA+PoulQCfqqK4OKDe1vi0oAgiSbvAQl4DoCnd4ANmb5k+5YevhouiHCiBCp1zUZZLJ6A28Ux7NBWioNxFuWUYh2syF+nOoQ0kyQ1bUUMYg8tFtm0SLj0MRTowh3fksCFsbYBj6sgx7Hd+5M8xlUDhd/v5mHh4zoTodQNRc5L/2nlT/eBSQPof1iIgkMsgYZjLllS0v1LPSdeGsnsreEVtqkWn/tPyLwcsqkcMxDKrhHbI3odlIkYngBLGqLuBWLVE52pihdCbGrVwpG4S0bpQ0qg==",
  "mobile": "yJ2hY5bc2g3P2pQyca/ER6VYQ8TGMj/VN42h9xkh/3jAwJQtZEspnhrtEKqwFXt1+8budi64CPlUEzbkwUsCotIOMm8idfSX+SQyb8VlqLxxIkAzGvmXjWrbQUNEUWnnJjzkIjweNmj8GJ2u0uRdrAGpBc1vMoMz5XD2SGfFttvmziTtucq5w2dOoAPOni4Bl7sfii3Qyo8Szl1/tXNnZbDZi8HH9Cpajno4pFiu6mQDVTkkyDHTqyo7Bv3IFpdNYiRDAZ1yh1cBOfufMy1gSZQetCwETFxdsOgw7JvKL/gEN+RAFKZF2oUriCsAkYYbxW1cfrqa/YRXUw0ho+n4Jw==",
  "countryCode": "+91 ",
  "pinCode": "110001",
  "address": "9th Floor, Tower-l, Jeevan Bharati Building, Connaught Place, New Delhi - 110001"
}
```
Responses
Return transaction id in case of success
**Example for Responses**
```
{
  "sessionId": "31216fed-4a23-4a18-ac89-03c9f3a0bf89"
}
```

3. **/v1/apps/generate/otp**
Explanation - Api Accepts Mobile Number/Email and then Generates OTP for it. Request Body - Required Response - Api Accepts Mobile Number/Email and then Generates OTP for it. if number/email id not found then throws error.

Note :

1. OTP will be valid for 10 Minutes only
Parameters 

No Parameters

Request body (In application/JSON)

**Example for Request body**
```
{
  "value": "yJ2hY5bc2g3P2pQyca/ER6VYQ8TGMj/VN42h9xkh/3jAwJQtZEspnhrtEKqwFXt1+8budi64CPlUEzbkwUsCotIOMm8idfSX+SQyb8VlqLxxIkAzGvmXjWrbQUNEUWnnJjzkIjweNmj8GJ2u0uRdrAGpBc1vMoMz5XD2SGfFttvmziTtucq5w2dOoAPOni4Bl7sfii3Qyo8Szl1/tXNnZbDZi8HH9Cpajno4pFiu6mQDVTkkyDHTqyo7Bv3IFpdNYiRDAZ1yh1cBOfufMy1gSZQetCwETFxdsOgw7JvKL/gEN+RAFKZF2oUriCsAkYYbxW1cfrqa/YRXUw0ho+n4Jw==",
  "authMode": "MOBILE_OTP / EMAIL_OTP"
}
```
Responses

Return transaction id in case of success

**Example for Responses**
```
{
  "sessionId": "31216fed-4a23-4a18-ac89-03c9f3a0bf89"
}
```

3. **/v1/apps/resend/otp**
Explanation - Api Accepts Transaction Number and then Resend OTP for it. Request Body - Required Response - Api Accepts Transaction Number and then Resend OTP for it. if transaction number not found then throws error.
Parameters 

No Parameters

Request body (In application/JSON)

**Example for Request body**
```
{
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```
Responses

Return transaction id in case of success

**Example for Responses**
```
{
  "success": "true",
  "sessionId": "16a18568-7c86-49a7-a95c-f1671cd04a94"
}
```

4. **/v1/apps/validate/otp**
API to verify the Mobile/Email OTP
Request
Below is the Request Parameters description

Attributes	Description
sessionId * required	Session number, Based on UUID.
value * required	Value reviced on the mobile number.
Note :

1. OTP must be in encrypted form, Plain text form OTP is not allowed
Parameters 

No Parameters

Request body (In application/JSON)

**Example for Request body**
```
{
  "value": "tSCaVUjHwHiMVCokz7u3ogfop5r7ON5GmVY4rJNaQhoVAMlZl5lDqbb4vobfFMsQ1zO404gkWqPqLoDCdavx+JJ5pxprDpRo+PbeV44q51xr5OoNW2ITy9x6WM81KF9o7OnIU3FOGg09jqcJ/By3S8ICWxzJDKVwCJPehHtjhSFiy+mdWEjKkBTrEWJRTy3ZOkij+fskm+JjLoJlIF0TmA94Jb/avX0/LrnacpWEYWAHd0R/8/HIeITVNwG5hnsuRyIcIKKy7bEuYul8wJDD8RPBhL/gIAV4c5zDCb518o1MJGQtNg8Yf/zcROdaynWrBHIh2tacPrxmLHiZHD+BHQ==",
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

Responses

Return Transaction Number in case of success

**Example of Responses**
```
{
  "mappedPhrAddress": "[user@abdm, user2@abdm]",
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```


