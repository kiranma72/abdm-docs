---
title: "Sign Up or Sign in using PHR Addr"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---

# Sign up or Sign in using PHR Address
# Sign up/Registration in PHR App
The PHR mobile application developed by ABDM is now known as ABHA mobile application and has been taken as a reference PHR application. In this application, by registration we means creating ABHA address aka PHR address, which is an easy to remember PHR address along with its password to login. 
In the ABHA app which is a reference app, registration can be done by two ways:
1. KYC Verified registration (Aadhar/DL/PAN)
2. Self declared registration (Mobile or Email)

## Registration via ABHA Number (KYC-Verified)
For registering using ABHA number, individual has to enter the 14-digit ABHA number and autheticate either via Aadhar OTP or Mobile OTP. 
After validating the OTP, the individual's profile details are auto populated from ABHA system. Already linked ABHA addresses will be displayed along with the option of creating new ABHA address. Individual can either choose already linked ABHA addresses to login or can create new ABHA address.
For creating new ABHA address, individual can choose an ABHA address from the suggestions displayed based on the user profile details or can create a different ABHA address as per ABHA Address creation policy, along with password. New ABHA address will be created for the given ABHA number and user can directly login.

<img width="184" alt="Picture1" src="https://user-images.githubusercontent.com/105836429/169759881-3f40a1c9-d442-4a63-beec-eaae5ad7f4ab.png">  <img width="184" alt="Picture2" src="https://user-images.githubusercontent.com/105836429/169759890-cb9fce56-f1e3-454a-bba4-553718d0e3f7.png">  <img width="184" alt="Picture3" src="https://user-images.githubusercontent.com/105836429/169759894-63a71fe4-74c4-431a-98a1-fc842fadf9fe.jpg">  <img width="184" alt="Picture4" src="https://user-images.githubusercontent.com/105836429/169759898-50a3cf78-ce1c-42ee-b5de-707a43c2f14e.png">  <img width="184" alt="Picture5" src="https://user-images.githubusercontent.com/105836429/169759900-67a02408-25a1-432f-8f8f-47ea9499a66d.png">

Swagger link for APIs: https://sandbox.abdm.gov.in/swagger/ndhm-phr-app2.yaml

**APIs for registering using ABHA number**
1. **URL: /v1/apps/registration/hid/confirm-init**

*Explanation* - Api Checks Health ID Number to find User.

*Request Body* - Required

*Response* - Retrun session in case of success against request.

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example for request body**
```
{
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "value": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI="
}
```
*Responses*

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

2. **URL:/v1/apps/create/registration/hid/create/phrAddress**

*Parameters*

No Parameters

*Request body* (In application/JSON)

**Example for request body**
```
{
  "alreadyExistedPHR": true,
  "password": "HNceo964MVndrs8Z2oMtzIsmmbzagveHbWkDsDKskTue+/YZhHHrMon19J03ggU457upzWMIX0nU3d38xjB3FxA2qWCVmvLZ98A9l0y3i33vq1ywu9cORGF4OEqV8l7H9h4tDnLGDHnbOh9ct85VfOohP4p73lqW6WQSMYcU+xkBfEsRj42pWL19EVsE1UULtQE8gYY1B0SeM63svUp1kQ4Pt5hdgKxibYBq+hRcck2PkEIhp2N7AkjH4Tf+AhXU9956WLwjKgAKMk7K4+Zv8JtxYCcblQitbpN4ImPH5edf4mO5R/L9RpdAVSllAQQfPIDlp5ZGOZ1GrSmhzOSP3g==",
  "phrAddress": "user@abdm",
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```
*Responses*

OK

**Example for Response**
```
{
  "phrAdress": "user@abdm",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
}
```

3. **URL: /v1/apps/registration/hid/auth-init**

*Explanation* - Api Checks Health ID Number to find User.

*Request Body* - Required

*Response* - Retrun transaction in case of success against request.

*Parameters* 

No Parameters

*Request body* (In application/JSON)

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
*Responses*

Return status as true alone with partail details of Health id number in case of success

**Example for Response**
```
{
  "sessionId": "31216fed-4a23-4a18-ac89-03c9f3a0bf89"
}
```

4. **URL: /v1/apps/registration/hid/search/auth-mode**

*Explanation* - Api Checks Health ID Number to find User.

*Request Body* - Required

*Response* - Retrun partial details of Health ID Number.

*Parameters*

No Parameters

*Request body* (In application/JSON)

**Example for request body**
```
{
  "healhtIdNumber": "11-1111-1111-1111"
}
```
*Responses*

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

### Registration via Mobile Number (Self-Verified)
For registering using mobile number, individual has to enter the mobile number and autheticate via OTP.  
After validating the OTP, list of already linked ABHA addresses will be displayed along with the option of creating new ABHA address. 
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

<img width="184" alt="Picture6" src="https://user-images.githubusercontent.com/105836429/169763808-1b2ec097-7e28-4b71-a68b-c98600ed5a0a.png">  <img width="184" alt="Picture10" src="https://user-images.githubusercontent.com/105836429/169765445-617a9190-3d0e-4d6d-97f0-4a3539e2a326.png">  <img width="184" alt="Picture8" src="https://user-images.githubusercontent.com/105836429/169763823-7d033d5e-3a9f-4a6f-b467-a860a19dc5e9.jpg">  <img width="184" alt="Picture9" src="https://user-images.githubusercontent.com/105836429/169764605-f5521dbd-d1c6-4205-b8ed-4cb4552f9a3b.png">  <img width="184" alt="Picture7" src="https://user-images.githubusercontent.com/105836429/169763818-ca8338c2-d02e-40b3-bab3-4f8f3bbae764.jpg">

#### Registration via Email ID (Self-Verified)
For registering using Email ID, individual has to enter the Email ID and autheticate via OTP.  
After validating the OTP, list of already linked ABHA addresses will be displayed along with the option of creating new ABHA address. 
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

<img width="184" alt="Picture11" src="https://user-images.githubusercontent.com/105836429/169766759-ef6210e7-6e42-4c80-870e-f46af9d3cd34.png">  <img width="184" alt="Picture12" src="https://user-images.githubusercontent.com/105836429/169766767-81865de8-30e7-48e1-93ed-7e99edc0d314.png">  <img width="184" alt="Picture13" src="https://user-images.githubusercontent.com/105836429/169766773-66abe7d9-420d-4a51-a2e9-acfafea1a8c1.jpg">  <img width="184" alt="Picture14" src="https://user-images.githubusercontent.com/105836429/169766778-ba5e4050-051a-495a-8743-de6170fab1f9.png">  <img width="184" alt="Picture15" src="https://user-images.githubusercontent.com/105836429/169766803-7ec3513b-6897-4381-9d35-bf2fcaffde6d.png">

Swagger link for APIs: https://sandbox.abdm.gov.in/swagger/ndhm-phr-app2.yaml

**APIs for registering using Mobile number or Email ID**
1. **URL: /v1/apps/create/phrAddress**

To Register the beneficiary.

Beneficiary data required to pass in the request

*Request*

Below is the Request Parameters description

*Attributes	Description*

sessionId * required	Session Id, Based on UUID.
phrAddress * required	PHR address of the Beneficiary or user
password * required	Password for the account. Same will be used to login to PHR Account. Password must contain an uppercase, a lowercase, a number, a special character (@,_$,#) and at least 8 or more characters. It should not contain any sequences (like 123)

Note :

1. Password must be in encrypted form, Plain text form Password is not allowed in request
*Parameters*

No Parameters

*Request body* (In application/JSON)

**Example for Request body**
```
{
  "alreadyExistedPHR": true,
  "password": "HNceo964MVndrs8Z2oMtzIsmmbzagveHbWkDsDKskTue+/YZhHHrMon19J03ggU457upzWMIX0nU3d38xjB3FxA2qWCVmvLZ98A9l0y3i33vq1ywu9cORGF4OEqV8l7H9h4tDnLGDHnbOh9ct85VfOohP4p73lqW6WQSMYcU+xkBfEsRj42pWL19EVsE1UULtQE8gYY1B0SeM63svUp1kQ4Pt5hdgKxibYBq+hRcck2PkEIhp2N7AkjH4Tf+AhXU9956WLwjKgAKMk7K4+Zv8JtxYCcblQitbpN4ImPH5edf4mO5R/L9RpdAVSllAQQfPIDlp5ZGOZ1GrSmhzOSP3g==",
  "phrAddress": "user@abdm",
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```
*Responses*

Return user token id in case of success

**Example for Responses**
```
{
  "phrAdress": "user@abdm",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
}
```

2. **URL: /v1/apps/registration/details**

To Register the beneficiary.

Beneficiary data required to pass in the request

*Request*

Below is the Request Parameters description

*Attributes	Description*

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
*Parameters*

No Parameters

*Request body* (In application/JSON)

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
*Responses*

Return transaction id in case of success

**Example for Responses**
```
{
  "sessionId": "31216fed-4a23-4a18-ac89-03c9f3a0bf89"
}
```

3. **URL: /v1/apps/generate/otp**

*Explanation* - Api Accepts Mobile Number/Email and then Generates OTP for it. 

*Request Body* - Required Response 

Api Accepts Mobile Number/Email and then Generates OTP for it. if number/email id not found then throws error.

Note :

1. OTP will be valid for 10 Minutes only
*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example for Request body**
```
{
  "value": "yJ2hY5bc2g3P2pQyca/ER6VYQ8TGMj/VN42h9xkh/3jAwJQtZEspnhrtEKqwFXt1+8budi64CPlUEzbkwUsCotIOMm8idfSX+SQyb8VlqLxxIkAzGvmXjWrbQUNEUWnnJjzkIjweNmj8GJ2u0uRdrAGpBc1vMoMz5XD2SGfFttvmziTtucq5w2dOoAPOni4Bl7sfii3Qyo8Szl1/tXNnZbDZi8HH9Cpajno4pFiu6mQDVTkkyDHTqyo7Bv3IFpdNYiRDAZ1yh1cBOfufMy1gSZQetCwETFxdsOgw7JvKL/gEN+RAFKZF2oUriCsAkYYbxW1cfrqa/YRXUw0ho+n4Jw==",
  "authMode": "MOBILE_OTP / EMAIL_OTP"
}
```
*Responses*

Return transaction id in case of success

**Example for Responses**
```
{
  "sessionId": "31216fed-4a23-4a18-ac89-03c9f3a0bf89"
}
```

3. **URL: /v1/apps/resend/otp**

*Explanation* - Api Accepts Transaction Number and then Resend OTP for it. 

*Request Body* - Required Response 

Api Accepts Transaction Number and then Resend OTP for it. if transaction number not found then throws error.
*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example for Request body**
```
{
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```
*Responses*

Return transaction id in case of success

**Example for Responses**
```
{
  "success": "true",
  "sessionId": "16a18568-7c86-49a7-a95c-f1671cd04a94"
}
```

4. **URL: /v1/apps/validate/otp**
API to verify the Mobile/Email OTP
Request
Below is the Request Parameters description

*Attributes	Description*
sessionId * required	Session number, Based on UUID.
value * required	Value reviced on the mobile number.

Note :

1. OTP must be in encrypted form, Plain text form OTP is not allowed

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example for Request body**
```
{
  "value": "tSCaVUjHwHiMVCokz7u3ogfop5r7ON5GmVY4rJNaQhoVAMlZl5lDqbb4vobfFMsQ1zO404gkWqPqLoDCdavx+JJ5pxprDpRo+PbeV44q51xr5OoNW2ITy9x6WM81KF9o7OnIU3FOGg09jqcJ/By3S8ICWxzJDKVwCJPehHtjhSFiy+mdWEjKkBTrEWJRTy3ZOkij+fskm+JjLoJlIF0TmA94Jb/avX0/LrnacpWEYWAHd0R/8/HIeITVNwG5hnsuRyIcIKKy7bEuYul8wJDD8RPBhL/gIAV4c5zDCb518o1MJGQtNg8Yf/zcROdaynWrBHIh2tacPrxmLHiZHD+BHQ==",
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

*Responses*

Return Transaction Number in case of success

**Example of Responses**
```
{
  "mappedPhrAddress": "[user@abdm, user2@abdm]",
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```


# Sign-in/Login in PHR App

The PHR mobile application developed by ABDM is now known as ABHA mobile application and has been taken as a reference PHR application. In this application, by login we means login into application using ABHA address aka PHR address, which is an easy to remember PHR address along with its password. 
In the ABHA app which is a reference app, login can be done by four ways:
1. Login via Mobile number
2. Login via ABHA address
3. Login via Email ID
4. Login via ABHA number

## Login via Mobile Number
Individual can login by entering the registered mobile number and validating it by the OTP. Once the mobile number is validated, the list of linked ABHA addresses will be displayed and individual can login by selecting any of the ABHA addresses. 

<img width="184" alt="Picture16" src="https://user-images.githubusercontent.com/105836429/169952732-99825807-41fc-4801-81b7-3bc8d5c2b18c.png">  <img width="184" alt="Picture17" src="https://user-images.githubusercontent.com/105836429/169952741-ec782508-4912-4aae-a96c-3df4cf004105.png">  <img width="184" alt="Picture18" src="https://user-images.githubusercontent.com/105836429/169952746-e56b619c-626b-46d4-8045-b6b9aab129b9.jpg">

Swagger link for APIs: https://sandbox.abdm.gov.in/swagger/ndhm-phr-app2.yaml

**APIs for login via mobile number**

1. **URL: /v1/apps/login/hid/auth-init**

*Explanation* - Api Accepts PHR ADDRESS and then Generates OTPbased on Authentication mode for it. 

*Request Body* - Required Response - Api Accepts HealthId Number and then Generates OTPbased on the auth methods for it. if number not found then throws error.

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
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
*Responses*

Return transaction id in case of success

**Example of Responses**
```
{
  "transactionId": "1431fa4f-82b4-4cba-bdc0-770e9178f644",
  "requesterId": "IN041XX",
  "authMode": "MOBILE_OTP",
  "error": null
}
```

2. **URL: /v1/apps/login/mobileEmail/auth-confirm**

fetch the User token

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "patientId": "user@abdm",
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "requesterId": "IN0401XX"
}
```
*Responses*
	
Return list of phr address mapped with mobile in case of success

**Example of Responses**
```
{
  "token": "Bearer eyJhbGciOiJSUzUxMiJ9.eyJzdWIiOiJzaHViaGFuc2h1QGFiZG0iLCJjbGllbnRJZCI6IiIsInJlcXVlc3RlcklkIjoiUEhSLVsdfsdfsdfsdfdsfsfszAtMDA4Mi00ZGJlLTk3N2MtMjUxY2YyMWZiOWFhIn0.DOmjJzM1KwfdgDSg_JiHvomo5_sOwqTgG2vMyaM-c1XMCPklR-0FdWKMipIjNVycoF_sdfdfsdsfvsdY6WAqk2fM3T0d8Z9cycuavzSynT4mtNNcHX78y4OAu53mpTsTpesA4s6dK8IAcN9ir9T7Cnr5k4393i5ZUTOTs9Fq1wLPR87YzfJ6-tUgOIDdfJiGzEew2vIz_wt481ShQiIeHOG5PPCPC-H1JhblqRzijFJEX2G0zvolwC8cO9ATBWZlbOxq9gmENzYMAY1y1IBb8uO56zeldiVf0-_Pw4f8nP90nlyQrGoYfut3HuK-jmL7nUBs7Y0gufUiFw8gAIEg"
}
```

3. **URL: /v1/apps/login/mobileEmail/auth-init**

*Explanation* - Api Accepts Mobile/Email address and then generates OTP for it. 

*Request Body* - Required Response - Api Accepts PHR ADDRESS and then generates OT Pbased on the auth methods for it. if number not found then throws error.

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "value": "yJ2hY5bc2g3P2pQyca/ER6VYQ8TGMj/VN42h9xkh/3jAwJQtZEspnhrtEKqwFXt1+8budi64CPlUEzbkwUsCotIOMm8idfSX+SQyb8VlqLxxIkAzGvmXjWrbQUNEUWnnJjzkIjweNmj8GJ2u0uRdrAGpBc1vMoMz5XD2SGfFttvmziTtucq5w2dOoAPOni4Bl7sfii3Qyo8Szl1/tXNnZbDZi8HH9Cpajno4pFiu6mQDVTkkyDHTqyo7Bv3IFpdNYiRDAZ1yh1cBOfufMy1gSZQetCwETFxdsOgw7JvKL/gEN+RAFKZF2oUriCsAkYYbxW1cfrqa/YRXUw0ho+n4Jw==",
  "purpose": "CM_ACCESS",
  "authMode": "MOBILE_OTP",
  "requester": {
    "type": "PHR",
    "id": "IN0400XX"
  }
}
```
*Responses*
	
Return transaction id in case of success

**Example of Responses**
```
{
  "transactionId": "1431fa4f-82b4-4cba-bdc0-770e9178f644",
  "requesterId": "IN041XX",
  "authMode": "MOBILE_OTP",
  "error": null
}
```

4. **URL: /v1/apps/login/mobileEmail/pre-Verify**

*Explanation* - Api Accepts Transaction Number and OTP(Encrypted form) for it. 

*Request Body* - Required

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "authcode": "tSCaVUjHwHiMVCokz7u3ogfop5r7ON5GmVY4rJNaQhoVAMlZl5lDqbb4vobfFMsQ1zO404gkWqPqLoDCdavx+JJ5pxprDpRo+PbeV44q51xr5OoNW2ITy9x6WM81KF9o7OnIU3FOGg09jqcJ/By3S8ICWxzJDKVwCJPehHtjhSFiy+mdWEjKkBTrEWJRTy3ZOkij+fskm+JjLoJlIF0TmA94Jb/avX0/LrnacpWEYWAHd0R/8/HIeITVNwG5hnsuRyIcIKKy7bEuYul8wJDD8RPBhL/gIAV4c5zDCb518o1MJGQtNg8Yf/zcROdaynWrBHIh2tacPrxmLHiZHD+BHQ==",
  "requesterId": "IN0410XX"
}
```

*Responses*
	
Return list of phr address mapped with mobile in case of success

**Example of Responses**
```
{
  "mappedPhrAddress": "[user@abdm, user2@abdm]",
  "mobileEmail": "9988776XX5",
  "requesterId": "IN0410XX",
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

5. **URL: /v1/apps/phrAddress/auth-init**

*Explanation* - Api Accepts PHR ADDRESS and then Generates OTPbased on Authentication mode for it.

*Request Body* - Required Response - Api Accepts PHR ADDRESS and then Generates OTPbased on the auth methods for it. if number not found then throws error.

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "patientId": "hinapatel@sbx",
  "purpose": "CM_ACCESS",
  "authMode": "MOBILE_OTP",
  "requester": {
    "type": "PHR",
    "id": "IN0400XX"
  }
}
```

*Responses*
	
Return transaction id in case of success

**Example of Responses**
```
{
  "transactionId": "b6547f6a-f0d1-4f6f-b82b-05f681b4d1f7",
  "requesterId": "IN0400XX",
  "authMode": "AADHAAR_OTP",
  "error": null
}
```
6. **URL: /v1/apps/phrAddress/auth-confirm**

*Explanation* - Api Accepts Transaction Id and Passowrd, Mobile/Email OTP based on Auth methods, Plain text credentails is not allowed. 

*Request Body* - Required

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "transactionId": "de277b66-00ea-4a4a-a29f-bb9a467960aa",
  "authCode": "2xxWA2g4HeLZsG3NB9/Zx676BIAXZaCHZU3LkrXxV0DSCaT1dQpKsd/Nq6tw6yjSOXiY8vM9GJpZ3gnkBttp47ciwVjM7iIKXKZghjuStDxIabUjEA5OdQZkLdiXp0t185s59tfOnKz1FsJeOPBzhM6qAEbn7EgMZounP3aZrS16FQrWahLNVgrxeVOrfg7HgZcwK+EHTP8q8Z9Ya4sW4sdsM3Aptkb1aBpj8j/G36+n9xNEoWTljfCeHdgpwKzWr2yU72ZLUXSEykA722H8NM8L982HNiLlOnBbmoaijMo50MKFse9pmSlveIQGPl3uz/NtAy+5sKLjtt31AR45sQ==",
  "requesterId": "IN0400XX"
}
```

*Responses*
	
Return user Token id in case of success

**Example of Responses**
```
{
  "token": "string"
}
```

7. **URL: /v1/apps/login/hid/search/auth-mode**

*Explanation* - Api Checks Health ID Number to find User.

*Request Body* - Required

*Response* - Retrun partial details of Health ID Number.

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "healthIdNumber": "11-1111-1111-1111",
  "yearOfBirth": "1994"
}
```
*Responses*
	
Return status as true alone with partail details of Health id number in case of success

**Example of Responses**
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

8. **URL: /v1/apps/phrAddress/search/auth-mode**

*Responses*
	
Return PHR ADDRESS Authentication method Details in case of success

**Example of Responses**
```
{
  "authMethods": "[PASSWORD, MOBILE_OTP, EMAIL_OTP]",
  "phrAddress": "user@abdm"
}
```

### Login via ABHA address

Individual can login by entering the ABHA address and validating it either by OTP or by using the password. Once the ABHA address is validated, individual can login into the account.

<img width="184" alt="Picture19" src="https://user-images.githubusercontent.com/105836429/169953341-bb05604f-9bbc-4897-9bc6-91720edb54df.png">  <img width="184" alt="Picture20" src="https://user-images.githubusercontent.com/105836429/169953345-002248eb-b603-4e1f-a1c9-874b13f6e49e.png">  <img width="184" alt="Picture18" src="https://user-images.githubusercontent.com/105836429/169952746-e56b619c-626b-46d4-8045-b6b9aab129b9.jpg">

Swagger link for APIs: https://sandbox.abdm.gov.in/swagger/ndhm-phr-app2.yaml

**APIs for login via ABHA address**

1. **URL: /v1/apps/login/hid/auth-init**

*Explanation* - Api Accepts PHR ADDRESS and then Generates OTPbased on Authentication mode for it. 

*Request Body* - Required Response - Api Accepts HealthId Number and then Generates OTPbased on the auth methods for it. if number not found then throws error.

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
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
*Responses*
Return transaction id in case of success

**Example of Responses**

```
{
  "transactionId": "1431fa4f-82b4-4cba-bdc0-770e9178f644",
  "requesterId": "IN041XX",
  "authMode": "MOBILE_OTP",
  "error": null
}
```

2. **URL: /v1/apps/login/mobileEmail/auth-confirm**

fetch the User token

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "patientId": "user@abdm",
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "requesterId": "IN0401XX"
}
```
*Responses*
	
Return list of phr address mapped with mobile in case of success

**Example of Responses**
```
{
  "token": "Bearer eyJhbGciOiJSUzUxMiJ9.eyJzdWIiOiJzaHViaGFuc2h1QGFiZG0iLCJjbGllbnRJZCI6IiIsInJlcXVlc3RlcklkIjoiUEhSLVsdfsdfsdfsdfdsfsfszAtMDA4Mi00ZGJlLTk3N2MtMjUxY2YyMWZiOWFhIn0.DOmjJzM1KwfdgDSg_JiHvomo5_sOwqTgG2vMyaM-c1XMCPklR-0FdWKMipIjNVycoF_sdfdfsdsfvsdY6WAqk2fM3T0d8Z9cycuavzSynT4mtNNcHX78y4OAu53mpTsTpesA4s6dK8IAcN9ir9T7Cnr5k4393i5ZUTOTs9Fq1wLPR87YzfJ6-tUgOIDdfJiGzEew2vIz_wt481ShQiIeHOG5PPCPC-H1JhblqRzijFJEX2G0zvolwC8cO9ATBWZlbOxq9gmENzYMAY1y1IBb8uO56zeldiVf0-_Pw4f8nP90nlyQrGoYfut3HuK-jmL7nUBs7Y0gufUiFw8gAIEg"
}
```

3. **URL: /v1/apps/login/mobileEmail/auth-init**

*Explanation* - Api Accepts Mobile/Email address and then Generates OTP for it. 

*Request Body* - Required Response - Api Accepts PHR ADDRESS and then Generates OTPbased on the auth methods for it. if number not found then throws error.

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "value": "yJ2hY5bc2g3P2pQyca/ER6VYQ8TGMj/VN42h9xkh/3jAwJQtZEspnhrtEKqwFXt1+8budi64CPlUEzbkwUsCotIOMm8idfSX+SQyb8VlqLxxIkAzGvmXjWrbQUNEUWnnJjzkIjweNmj8GJ2u0uRdrAGpBc1vMoMz5XD2SGfFttvmziTtucq5w2dOoAPOni4Bl7sfii3Qyo8Szl1/tXNnZbDZi8HH9Cpajno4pFiu6mQDVTkkyDHTqyo7Bv3IFpdNYiRDAZ1yh1cBOfufMy1gSZQetCwETFxdsOgw7JvKL/gEN+RAFKZF2oUriCsAkYYbxW1cfrqa/YRXUw0ho+n4Jw==",
  "purpose": "CM_ACCESS",
  "authMode": "MOBILE_OTP",
  "requester": {
    "type": "PHR",
    "id": "IN0400XX"
  }
}
```
*Responses*
	
Return transaction id in case of success

**Example of Responses**
```
{
  "transactionId": "1431fa4f-82b4-4cba-bdc0-770e9178f644",
  "requesterId": "IN041XX",
  "authMode": "MOBILE_OTP",
  "error": null
}
```

4. **URL: /v1/apps/login/mobileEmail/pre-Verify**

*Explanation* - Api Accepts Transaction Number and OTP(Encrypted form) for it. 

*Request Body* - Required

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "authcode": "tSCaVUjHwHiMVCokz7u3ogfop5r7ON5GmVY4rJNaQhoVAMlZl5lDqbb4vobfFMsQ1zO404gkWqPqLoDCdavx+JJ5pxprDpRo+PbeV44q51xr5OoNW2ITy9x6WM81KF9o7OnIU3FOGg09jqcJ/By3S8ICWxzJDKVwCJPehHtjhSFiy+mdWEjKkBTrEWJRTy3ZOkij+fskm+JjLoJlIF0TmA94Jb/avX0/LrnacpWEYWAHd0R/8/HIeITVNwG5hnsuRyIcIKKy7bEuYul8wJDD8RPBhL/gIAV4c5zDCb518o1MJGQtNg8Yf/zcROdaynWrBHIh2tacPrxmLHiZHD+BHQ==",
  "requesterId": "IN0410XX"
}
```

*Responses*
	
Return list of phr address mapped with mobile in case of success

**Example of Responses**
```
{
  "mappedPhrAddress": "[user@abdm, user2@abdm]",
  "mobileEmail": "9988776XX5",
  "requesterId": "IN0410XX",
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

5. **URL: /v1/apps/phrAddress/auth-init**

*Explanation* - Api Accepts PHR ADDRESS and then Generates OTPbased on Authentication mode for it.

*Request Body* - Required Response - Api Accepts PHR ADDRESS and then Generates OTPbased on the auth methods for it. if number not found then throws error.

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "patientId": "hinapatel@sbx",
  "purpose": "CM_ACCESS",
  "authMode": "MOBILE_OTP",
  "requester": {
    "type": "PHR",
    "id": "IN0400XX"
  }
}
```

*Responses*
	
Return transaction id in case of success

**Example of Responses**
```
{
  "transactionId": "b6547f6a-f0d1-4f6f-b82b-05f681b4d1f7",
  "requesterId": "IN0400XX",
  "authMode": "AADHAAR_OTP",
  "error": null
}
```
6. **URL: /v1/apps/phrAddress/auth-confirm**

*Explanation* - Api Accepts Transaction Id and Passowrd, Mobile/Email OTP based on Auth methods, Plain text credentails is not allowed. 

*Request Body* - Required

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "transactionId": "de277b66-00ea-4a4a-a29f-bb9a467960aa",
  "authCode": "2xxWA2g4HeLZsG3NB9/Zx676BIAXZaCHZU3LkrXxV0DSCaT1dQpKsd/Nq6tw6yjSOXiY8vM9GJpZ3gnkBttp47ciwVjM7iIKXKZghjuStDxIabUjEA5OdQZkLdiXp0t185s59tfOnKz1FsJeOPBzhM6qAEbn7EgMZounP3aZrS16FQrWahLNVgrxeVOrfg7HgZcwK+EHTP8q8Z9Ya4sW4sdsM3Aptkb1aBpj8j/G36+n9xNEoWTljfCeHdgpwKzWr2yU72ZLUXSEykA722H8NM8L982HNiLlOnBbmoaijMo50MKFse9pmSlveIQGPl3uz/NtAy+5sKLjtt31AR45sQ==",
  "requesterId": "IN0400XX"
}
```

*Responses*
	
Return user Token id in case of success

**Example of Responses**
```
{
  "token": "string"
}
```

7. **URL: /v1/apps/login/hid/search/auth-mode**

*Explanation* - Api Checks Health ID Number to find User.

*Request Body* - Required

Response - Retrun partial details of Health ID Number.

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "healthIdNumber": "11-1111-1111-1111",
  "yearOfBirth": "1994"
}
```
*Responses*
	
Return status as true alone with partail details of Health id number in case of success

**Example of Responses**
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

8. **URL: /v1/apps/phrAddress/search/auth-mode**

*Responses*
	
Return PHR ADDRESS Authentication method Details in case of success

**Example of Responses**
```
{
  "authMethods": "[PASSWORD, MOBILE_OTP, EMAIL_OTP]",
  "phrAddress": "user@abdm"
}
```

### Login via Email ID

Individual can login by entering the Email ID and validating it by the OTP. Once the Email ID is validated, the list of linked ABHA addresses will be displayed and individual can login by selecting any of the ABHA addresses.

<img width="184" alt="Picture21" src="https://user-images.githubusercontent.com/105836429/169953593-65c71a9a-7b35-4518-8a69-7204d34573b8.png">  <img width="184" alt="Picture22" src="https://user-images.githubusercontent.com/105836429/169953596-1ea31928-153b-4074-9eaa-f056dd3067a2.png">  <img width="184" alt="Picture23" src="https://user-images.githubusercontent.com/105836429/169953600-b9ce4955-bade-42b2-be91-ce3d14005580.png">  <img width="184" alt="Picture18" src="https://user-images.githubusercontent.com/105836429/169952746-e56b619c-626b-46d4-8045-b6b9aab129b9.jpg">

Swagger link for APIs: https://sandbox.abdm.gov.in/swagger/ndhm-phr-app2.yaml

**APIs for login via Email ID**

1. **URL: /v1/apps/login/hid/auth-init**

*Explanation* - Api Accepts PHR ADDRESS and then Generates OTPbased on Authentication mode for it. 

*Request Body* - Required Response - Api Accepts HealthId Number and then Generates OTPbased on the auth methods for it. if number not found then throws error.

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
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
*Responses*
Return transaction id in case of success

**Example of Responses**

```
{
  "transactionId": "1431fa4f-82b4-4cba-bdc0-770e9178f644",
  "requesterId": "IN041XX",
  "authMode": "MOBILE_OTP",
  "error": null
}
```

2. **URL: /v1/apps/login/mobileEmail/auth-confirm**

fetch the User token

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "patientId": "user@abdm",
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "requesterId": "IN0401XX"
}
```
*Responses*
	
Return list of phr address mapped with mobile in case of success

**Example of Responses**
```
{
  "token": "Bearer eyJhbGciOiJSUzUxMiJ9.eyJzdWIiOiJzaHViaGFuc2h1QGFiZG0iLCJjbGllbnRJZCI6IiIsInJlcXVlc3RlcklkIjoiUEhSLVsdfsdfsdfsdfdsfsfszAtMDA4Mi00ZGJlLTk3N2MtMjUxY2YyMWZiOWFhIn0.DOmjJzM1KwfdgDSg_JiHvomo5_sOwqTgG2vMyaM-c1XMCPklR-0FdWKMipIjNVycoF_sdfdfsdsfvsdY6WAqk2fM3T0d8Z9cycuavzSynT4mtNNcHX78y4OAu53mpTsTpesA4s6dK8IAcN9ir9T7Cnr5k4393i5ZUTOTs9Fq1wLPR87YzfJ6-tUgOIDdfJiGzEew2vIz_wt481ShQiIeHOG5PPCPC-H1JhblqRzijFJEX2G0zvolwC8cO9ATBWZlbOxq9gmENzYMAY1y1IBb8uO56zeldiVf0-_Pw4f8nP90nlyQrGoYfut3HuK-jmL7nUBs7Y0gufUiFw8gAIEg"
}
```

3. **URL: /v1/apps/login/mobileEmail/auth-init**

*Explanation* - Api Accepts Mobile/Email address and then Generates OTP for it. 

*Request Body* - Required Response - Api Accepts PHR ADDRESS and then Generates OTPbased on the auth methods for it. if number not found then throws error.

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "value": "yJ2hY5bc2g3P2pQyca/ER6VYQ8TGMj/VN42h9xkh/3jAwJQtZEspnhrtEKqwFXt1+8budi64CPlUEzbkwUsCotIOMm8idfSX+SQyb8VlqLxxIkAzGvmXjWrbQUNEUWnnJjzkIjweNmj8GJ2u0uRdrAGpBc1vMoMz5XD2SGfFttvmziTtucq5w2dOoAPOni4Bl7sfii3Qyo8Szl1/tXNnZbDZi8HH9Cpajno4pFiu6mQDVTkkyDHTqyo7Bv3IFpdNYiRDAZ1yh1cBOfufMy1gSZQetCwETFxdsOgw7JvKL/gEN+RAFKZF2oUriCsAkYYbxW1cfrqa/YRXUw0ho+n4Jw==",
  "purpose": "CM_ACCESS",
  "authMode": "MOBILE_OTP",
  "requester": {
    "type": "PHR",
    "id": "IN0400XX"
  }
}
```
*Responses*
	
Return transaction id in case of success

**Example of Responses**
```
{
  "transactionId": "1431fa4f-82b4-4cba-bdc0-770e9178f644",
  "requesterId": "IN041XX",
  "authMode": "MOBILE_OTP",
  "error": null
}
```

4. **URL: /v1/apps/login/mobileEmail/pre-Verify**

*Explanation* - Api Accepts Transaction Number and OTP(Encrypted form) for it. 

*Request Body* - Required

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "authcode": "tSCaVUjHwHiMVCokz7u3ogfop5r7ON5GmVY4rJNaQhoVAMlZl5lDqbb4vobfFMsQ1zO404gkWqPqLoDCdavx+JJ5pxprDpRo+PbeV44q51xr5OoNW2ITy9x6WM81KF9o7OnIU3FOGg09jqcJ/By3S8ICWxzJDKVwCJPehHtjhSFiy+mdWEjKkBTrEWJRTy3ZOkij+fskm+JjLoJlIF0TmA94Jb/avX0/LrnacpWEYWAHd0R/8/HIeITVNwG5hnsuRyIcIKKy7bEuYul8wJDD8RPBhL/gIAV4c5zDCb518o1MJGQtNg8Yf/zcROdaynWrBHIh2tacPrxmLHiZHD+BHQ==",
  "requesterId": "IN0410XX"
}
```

*Responses*
	
Return list of phr address mapped with mobile in case of success

**Example of Responses**
```
{
  "mappedPhrAddress": "[user@abdm, user2@abdm]",
  "mobileEmail": "9988776XX5",
  "requesterId": "IN0410XX",
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

5. **URL: /v1/apps/phrAddress/auth-init**

*Explanation* - Api Accepts PHR ADDRESS and then Generates OTPbased on Authentication mode for it.

*Request Body* - Required Response - Api Accepts PHR ADDRESS and then Generates OTPbased on the auth methods for it. if number not found then throws error.

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "patientId": "hinapatel@sbx",
  "purpose": "CM_ACCESS",
  "authMode": "MOBILE_OTP",
  "requester": {
    "type": "PHR",
    "id": "IN0400XX"
  }
}
```

*Responses*
	
Return transaction id in case of success

**Example of Responses**
```
{
  "transactionId": "b6547f6a-f0d1-4f6f-b82b-05f681b4d1f7",
  "requesterId": "IN0400XX",
  "authMode": "AADHAAR_OTP",
  "error": null
}
```
6. **URL: /v1/apps/phrAddress/auth-confirm**

*Explanation* - Api Accepts Transaction Id and Passowrd, Mobile/Email OTP based on Auth methods, Plain text credentails is not allowed. 

*Request Body* - Required

Note :

1. OTP will be valid for 10 Minutes only

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "transactionId": "de277b66-00ea-4a4a-a29f-bb9a467960aa",
  "authCode": "2xxWA2g4HeLZsG3NB9/Zx676BIAXZaCHZU3LkrXxV0DSCaT1dQpKsd/Nq6tw6yjSOXiY8vM9GJpZ3gnkBttp47ciwVjM7iIKXKZghjuStDxIabUjEA5OdQZkLdiXp0t185s59tfOnKz1FsJeOPBzhM6qAEbn7EgMZounP3aZrS16FQrWahLNVgrxeVOrfg7HgZcwK+EHTP8q8Z9Ya4sW4sdsM3Aptkb1aBpj8j/G36+n9xNEoWTljfCeHdgpwKzWr2yU72ZLUXSEykA722H8NM8L982HNiLlOnBbmoaijMo50MKFse9pmSlveIQGPl3uz/NtAy+5sKLjtt31AR45sQ==",
  "requesterId": "IN0400XX"
}
```

*Responses*
	
Return user Token id in case of success

**Example of Responses**
```
{
  "token": "string"
}
```

7. **URL: /v1/apps/login/hid/search/auth-mode**

*Explanation* - Api Checks Health ID Number to find User.

*Request Body* - Required

*Response* - Retrun partial details of Health ID Number.

*Parameters* 

No Parameters

*Request body* (In application/JSON)

**Example of Request body**
```
{
  "healthIdNumber": "11-1111-1111-1111",
  "yearOfBirth": "1994"
}
```
*Responses*
	
Return status as true alone with partail details of Health id number in case of success

**Example of Responses**
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

8. **URL: /v1/apps/phrAddress/search/auth-mode**

*Responses*
	
Return PHR ADDRESS Authentication method Details in case of success

**Example of Responses**
```
{
  "authMethods": "[PASSWORD, MOBILE_OTP, EMAIL_OTP]",
  "phrAddress": "user@abdm"
}
```

#### Login via ABHA number

Individual can login by entering the ABHA number and Year of Birth and validating it by the OTP. Once the ABHA number is validated, the list of linked ABHA addresses will be displayed and individual can login by selecting any of the ABHA addresses.

<img width="184" alt="Picture24" src="https://user-images.githubusercontent.com/105836429/169953882-68a5bf9a-9cb5-464e-b2a6-b26124228eac.png">  <img width="184" alt="Picture25" src="https://user-images.githubusercontent.com/105836429/169953886-6a254513-9f46-41cb-aff5-b1135b4573f9.png">  <img width="184" alt="Picture26" src="https://user-images.githubusercontent.com/105836429/169953889-f1d8385c-3e54-4823-a6dc-2d8c44845b28.png">  <img width="184" alt="Picture18" src="https://user-images.githubusercontent.com/105836429/169952746-e56b619c-626b-46d4-8045-b6b9aab129b9.jpg">

Swagger link for APIs: https://app.swaggerhub.com/apis-docs/abdm.abha/abha-service/1.0#/Profile/createPhrAdressWithHealthIdNumberUsingPOST

**URL: /v1/account/update/phr-address**

*Explanation* - API Accepts ABHA Number and Creates ABHA Address.

*Request Body* - Required

*Response* - API Accepts ABHA Number and Creates ABHA Address. Returns Error for Invalid/Incorrect Info..

*Parameters*

Name	Description
Accept-Language
string
(header)
Default value : en-US

X-Token *
string
(header)
x-example: Bearer X-Token
Auth Token

Example : Bearer X-Token

Bearer X-Token

*Responses*
	
Successfully Created PHR.

**Example of Responses**
```
string
```


