# Edit your profile 
User can view and edit his/her profile in the **View complete Profile** on dashboard. The screen displays QR code which user can use to share the information with HIP and can also download the ABHA card.
The screen also displays user details that are KYC verified (Aadhar verified profile) and cannot be edited such as
1. Name
2. Gender
3. DOB
Other details displayed are editable such as
1. Mobile                   
2. Email ID                 
3. Address 
- District
- State
- Pin Code                

In self-verified profile (Created by Mobile/Email ID), all the details can be edited. 

<img width="184" alt="5" src="https://user-images.githubusercontent.com/105836429/170986464-95da5a77-8873-4475-a1b8-999e1289daec.jpg"> <img width="184" alt="4" src="https://user-images.githubusercontent.com/105836429/170985406-0d380f0f-6b21-4ed6-81bc-bba488adf0a2.png">  <img width="184" alt="2" src="https://user-images.githubusercontent.com/105836429/170985380-9cf1c7ae-240c-4fe1-973f-d0785e25a52c.jpg">  <img width="184" alt="3" src="https://user-images.githubusercontent.com/105836429/170985382-48ffa642-b0c7-472b-bed7-f67ec7e48f8f.jpg">  

**Swagger link for API**: https://app.swaggerhub.com/apis-docs/abdm.abha/abha-service/1.0#/Integrated%20Programs/updateAccountInformationUsingPOST_1

**API for Edit profile**

*Explanation* - API Accepts Account Details and Updates it.

*Request Body* - Required

*Response* - API Accepts Account Details and Updates it. Returns Error for Invalid/Incorrect Account Details.

*Parameters*

Name	Description
Accept-Language
string
(header)
Default value : en-US

en-US
request *
object
(body)
request

**Example for request**
```
{
  "address": "b-14 someshwar nagar",
  "dayOfBirth": "31",
  "districtCode": "401",
  "email": "example@demo.com",
  "firstName": "kishan",
  "healthId": "deepakndhm",
  "healthIdNumber": "43-4221-5105-6749",
  "lastName": "singh",
  "middleName": "kumar",
  "monthOfBirth": "05",
  "password": "India@143",
  "pincode": 412306,
  "profilePhoto": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkJCQkJCQoLCwoODw0PDhQSERESFB4WFxYXFh4uHSEdHSEdLikxKCUoMSlJOTMzOUlUR0NHVGZbW2aBeoGoqOIBCQkJCQkJCgsLCg4PDQ8OFBIRERIUHhYXFhcWHi4dIR0dIR0uKTEoJSgxKUk5MzM5SVRHQ0dUZltbZoF6gaio4v/CABEIBLAHgAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwABBAUGB//aAAgBAQAAAADwawLpMspcK7qrlE5F0Vtul2bVywMUNeBHUkW/bmxvYELGuNjh2VDvixxo5ViljKjDRMoahCULjs2JCShjhjh2OGxo0Y2MoXHOLszsKLhw7tD99mpZQxj8xceofmLEKFwXLTIyHwY1Ls+iEotjHY0M0pjRYxtGj4VFKLPohQlFQyy4Qipc0XG9pS+CP/2Q==",
  "stateCode": "27",
  "subdistrictCode": "213",
  "townCode": "27",
  "villageCode": "412",
  "wardCode": "08",
  "yearOfBirth": "1994"
}
```

*Responses*

Show User Details in case of success

**Example of responses**
```
{
  "address": "b-14 someshwar nagar",
  "authMethods": "AADHAAR_OTP",
  "dayOfBirth": "31",
  "districtCode": "401",
  "districtName": "Pune",
  "email": "example@demo.com",
  "emailVerified": true,
  "firstName": "kishan",
  "gender": "Male",
  "healthId": "deepakndhm",
  "healthIdNumber": "43-4221-5105-6749",
  "kycPhoto": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI=",
  "kycVerified": true,
  "lastName": "singh",
  "middleName": "kumar",
  "mobile": "9545812125",
  "monthOfBirth": "05",
  "name": "kishan kumar singh",
  "new": true,
  "phrAddress": [
    "string"
  ],
  "pincode": "412306",
  "profilePhoto": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkJCQkJCQoLCwoODw0PDhQSERESFB4WFxYXFh4uHSEdHSEdLikxKCUoMSlJOTMzOUlUR0NHVGZbW2aBeoGoqOIBCQkJCQkJCgsLCg4PDQ8OFBIRERIUHhYXFhcWHi4dIR0dIR0uKTEoJSgxKUk5MzM5SVRHQ0dUZltbZoF6gaio4v/CABEIBLAHgAMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwABBAUGB//aAAgBAQAAAADwawLpMspcK7qrlE5F0Vtul2bVywMUNeBHUkW/bmxvYELGuNjh2VDvixxo5ViljKjDRMoahCULjs2JCShjhjh2OGxo0Y2MoXHOLszsKLhw7tD99mpZQxj8xceofmLEKFwXLTIyHwY1Ls+iEotjHY0M0pjRYxtGj4VFKLPohQlFQyy4Qipc0XG9pS+CP/2Q==",
  "stateCode": "27",
  "stateName": "MAHARASHTRA",
  "subDistrictCode": "213",
  "subdistrictName": "Baramati",
  "tags": {
    "additionalProp1": "string",
    "additionalProp2": "string",
    "additionalProp3": "string"
  },
  "townCode": "27",
  "townName": "Baramati",
  "verificationStatus": "verified",
  "verificationType": "testing",
  "villageCode": "412",
  "villageName": "Someshwar Nagar",
  "wardCode": "08",
  "wardName": "Sinhgad fort ward",
  "yearOfBirth": "1994"
}
```
