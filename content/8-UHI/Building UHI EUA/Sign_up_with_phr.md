---
title: "Sign In/Up with PHR Addr"
date: 2022-05-07T18:00:04+05:30
Weight: 1
draft: false
---

## Sign in with ABHA Number/Mobile Number

### Overview of the functionality
- User can login with mobile number/email ID linked to their ABHA ID/address
- OTP is sent to the user’s mobile number/email ID to authenticate the request
- User enters the OTP to authenticate the request.
- In case multiple ABHA numbers are linked to their number they can choose the account they want to login with.
- The user is displayed the linked ABHA addresses to their ABHA ID and proceeds to select one to login.

### Reference UI
<img width="613" alt="Screenshot 2022-06-01 at 5 43 10 PM" src="https://user-images.githubusercontent.com/98421565/171401789-bc5103f1-4b16-4ddc-bd44-360b51476976.png">

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

