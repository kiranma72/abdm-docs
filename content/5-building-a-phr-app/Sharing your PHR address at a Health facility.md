# Sharing your PHR address at a Health facility
User can share his/her profile using QR code scanner which is on the top right side of the screen. When clicked, it opens the new screen where details of user is 
displayed such as
- Name
- ABHA address
- Year of Birth
- Gender

User has also being provided with the option to share QR Code. User can also download and view his/her ABHA address card.

Along with the user's details, QR Code scanner is also displayed which user can use while visiting the hospital. Using the scanner, the user can scan a HIP QR Code pasted on the registration desk of the facility. User will scan the QR code and consent to sharing their ABHA number with the health facility
Post successful completion of the process patient is registered at the HIP thus saving time. 
 
<img width="184" alt="8" src="https://user-images.githubusercontent.com/105836429/171555990-9c3aecbd-bda7-4a6e-a967-1b5c4480a288.png">  <img width="184" alt="9" src="https://user-images.githubusercontent.com/105836429/171555994-08ce0a1b-2772-4648-bcf4-5be9a528940e.jpg">  <img width="184" alt="10" src="https://user-images.githubusercontent.com/105836429/171555995-4dc76bd4-2e44-46ad-9cb7-30822bce4d9c.jpg">  <img width="307" alt="11" src="https://user-images.githubusercontent.com/105836429/171555997-4333594c-6057-4fa7-bde8-09758d84a226.png">

**APIs for Sharing ABHA address**

*Swagger link*: https://app.swaggerhub.com/apis-docs/abdm.abha/abha-service/1.0#/

1. **/v1/account/qrCode**
Get Quick Response code in PNG format for this account.

Explanation - Api Accepts Auth Token and then returns Account Info for QR Code.

Request Body - Required

Responce - Api Accepts Auth Token and then returns Account Info for QR Code. Returns Error for Unauthorized Token.

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
x-example: Bearer XToken
Auth Token

Example : Bearer XToken

Bearer XToken

*Responses*

Return QR Code in Byte Array Form in case of success

*Example of Responses*
```
string
```
