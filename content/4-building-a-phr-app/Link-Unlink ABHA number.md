ABHA number is the uniquely generated 14 digit number which provides the strong identity to an individual, whereas ABHA address is use to share the health records of the individual with different healthcare providers and payers. Individual can link/Unlink ABHA number with the ABHA address to experience the benefits of both.  

# Link ABHA number

In link ABHA number flow, the ABHA address is linked with the ABHA number of the user. The link ABHA number is displayed just below the profile pic and when selected, user has to fill the ABHA number and validate it using either the Aadhar OTP or Mobile OTP linked to the ABHA number. Once the number is validated, the ABHA address will be linked to ABHA number.

<img width="184" alt="Picture27" src="https://user-images.githubusercontent.com/105836429/170210796-56073fd9-e7f7-4f2f-bf49-8315f29faa52.png">  <img width="184" alt="Picture28" src="https://user-images.githubusercontent.com/105836429/170210808-75a23352-83e3-4d77-bd45-ca07042e2f2a.png">  <img width="184" alt="Picture29" src="https://user-images.githubusercontent.com/105836429/170210812-9a578649-f0ec-4926-91e4-fb768314b381.png">

**Swagger URL**: https://app.swaggerhub.com/apis-docs/abdm.abha/abha-service/1.0#/ 

**APIs for Link ABHA number**

1. **URL:/v2/account/phr-linked**

*Explanation* - API links the given ABHA Address to the ABHA number and defines whether it is the preferred ABHA Address

*Request Body* - Required

*Parameters*
Name	Description
Accept-Language
string
(header)
Default value : en-US

en-US
X-Token *
string
(header)
x-example: Bearer X-Token
Auth Token

*Example* : Bearer X-Token

Bearer X-Token
phrLinkedOrDeLinkedRequestPayLoad *
object
(body)
phrLinkedOrDeLinkedRequestPayLoad

**Example**
```
{
  "phrAddress": "string",
  "preferred": true
}
```
*Responses*
	
Return status true in case of success
```
true
```

## Unlink ABHA number

In Unlink ABHA number flow, the ABHA address is unlinked with the ABHA number of the user. The unlink ABHA number is displayed just below the profile pic and when selected, system takes confirmation from the user before unlinking the ABHA number. Once the user provides the confirmation, he/she can validate using either the Aadhar OTP or Mobile OTP linked to the ABHA number. Once the number is validated, the ABHA address will be unlinked from the ABHA number.

<img width="184" alt="Picture30" src="https://user-images.githubusercontent.com/105836429/170220286-d202020a-fa20-45f0-a316-94c4ffdccc52.png">  <img width="184" alt="Picture31" src="https://user-images.githubusercontent.com/105836429/170220299-8290c94f-fd72-44c0-819a-94664c3f6bcf.jpg">  <img width="184" alt="Picture32" src="https://user-images.githubusercontent.com/105836429/170220303-794dc332-d9d5-449c-8a5d-606e412f8d6c.jpg">  <img width="184" alt="Picture33" src="https://user-images.githubusercontent.com/105836429/170220305-e086739a-df78-4bd6-a37d-c0618ae8b820.jpg">

**Swagger URL**: https://app.swaggerhub.com/apis-docs/abdm.abha/abha-service/1.0#/ 

### APIs for Unlinking ABHA number

1. **URL:/v2/account/phr-delinked**

*Explanation*- API delinks a given ABHA Address from the ABHA number

*Request Body* - Required

*Parameters*
Name	Description
Accept-Language
string
(header)
Default value : en-US

en-US
X-Token *
string
(header)
x-example: Bearer X-Token
Auth Token

*Example* : Bearer X-Token

Bearer X-Token
phrLinkedOrDeLinkedRequestPayLoad *
object
(body)
phrLinkedOrDeLinkedRequestPayLoad

**Example**
```
{
  "phrAddress": "string"
}
```

*Responses*
	
Return status true in case of success

**Example of Responses**
```
true
```
