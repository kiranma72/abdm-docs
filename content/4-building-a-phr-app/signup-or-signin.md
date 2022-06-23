---
title: "Sign Up or Sign in"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
Pre: "<b>4.1 </b>"
---

### Sign up / Sign in 

Every PHR App user needs to have an ABHA Address (also reffered to as PHR Address). The address looks like "username@hie-cm". Currently ABDM manages 2 HIE-CMs. The Sandbox HIE-CM @sbx and the production HIE-CM @abdm. PHR Apps use APIs provided by the HIE-CM to create a new ABHA address for users. 

The user chosen ABHA address has to be alphanumeric. The only numeric address allowed is 14 digits and that must be a valid ABHA number. 

### Recommended User Experience 

- User is requested to enter their mobile no / email id
- The mobile / email is validated via an OTP 
- All ABHA Addresses linked to the mobile / email is retrieved and presented to user.
- User can select an already created ABHA address and login OR
- User can create a new ABHA address linked to this mobile or email 
- PHR app should check & suggest PHR addressess that are available when creating a new address

This is demonstrated in the ABHA PHR reference app 

![Sequence](FlowSequence.png)

### Multiple ABHA Addresses for same user

Users are allowed to create multiple ABHA addresses as per their convienence / requirement. ABDM requires PHR apps to educate users that is it better to maintain only one ABHA address and link all health records to this address. 

The ABDM HIE-CM restricts the number of ABHA addresses that can be linked to a single mobile number to 4

### API Sequence for Registration using Health ID number. 

**API Sequence Diagram for Registration using Health ID number**
![Sequence](APISequenceDiagram.png)

Swagger link- https://sandbox.abdm.gov.in/swagger/ndhm-phr-app2.yaml/

1. Search a user by Health ID Number.

**URL**: https://dev.abdm.gov.in/cm/v1/apps/registration/hid/search/auth-mode

**METHOD**:POST

**HEADERS**:

**Request Body**:
```
{
  "healhtIdNumber": "11-1111-1111-1111"
}
```

**Response**:

200 Return status as true alone with partail details of Health id number in case of success

201 Created

2. It will create the transaction and send the otp on mobile number

**URL**: https://dev.abdm.gov.in/cm/v1/apps/registration/hid/auth-init

**Method**: POST

**HEADERS**:

**Request Body**:
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

**Response**:

200 Return status as true alone with partail details of Health id number in case of success

201 Created

3. It will the transaction and send the otp on mobile number

**URL**: https://dev.abdm.gov.in/cm/v1/apps/registration/hid/confirm-init 

**Method**: POST

**HEADERS**:

**Request Body**:
```
{
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "value": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI="
}
```

**Response**:

200 Return status as true alone with partail details of Health id number in case of success

201 Created

4. **URL**: https://dev.abdm.gov.in/cm/v1/apps/create/registration/hid/create/phrAddress

**Method**: POST

**HEADERS**:

**Request Body**:
```
{
  "alreadyExistedPHR": true,
  "password": "HNceo964MVndrs8Z2oMtzIsmmbzagveHbWkDsDKskTue+/YZhHHrMon19J03ggU457upzWMIX0nU3d38xjB3FxA2qWCVmvLZ98A9l0y3i33vq1ywu9cORGF4OEqV8l7H9h4tDnLGDHnbOh9ct85VfOohP4p73lqW6WQSMYcU+xkBfEsRj42pWL19EVsE1UULtQE8gYY1B0SeM63svUp1kQ4Pt5hdgKxibYBq+hRcck2PkEIhp2N7AkjH4Tf+AhXU9956WLwjKgAKMk7K4+Zv8JtxYCcblQitbpN4ImPH5edf4mO5R/L9RpdAVSllAQQfPIDlp5ZGOZ1GrSmhzOSP3g==",
  "phrAddress": "user@abdm",
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response**:

200 OK

201 Created

#### API Sequence for Registration of PHR Address using Mobile/Email .

**API Sequence Diagram**
![Sequence](https://github.com/kiranma72/abdm-docs/blob/main/content/4-building-a-phr-app/APIsequencediagramRegistrationofPHRAddressusingMobile%26Email%20.png)

1. Generate Mobile/Email OTP to start registration transaction

**URL: https://dev.abdm.gov.in/cm/v1/apps/generate/otp**

**Method**: POST

**HEADERS**: 

**Request body**
```
{
  "value": "yJ2hY5bc2g3P2pQyca/ER6VYQ8TGMj/VN42h9xkh/3jAwJQtZEspnhrtEKqwFXt1+8budi64CPlUEzbkwUsCotIOMm8idfSX+SQyb8VlqLxxIkAzGvmXjWrbQUNEUWnnJjzkIjweNmj8GJ2u0uRdrAGpBc1vMoMz5XD2SGfFttvmziTtucq5w2dOoAPOni4Bl7sfii3Qyo8Szl1/tXNnZbDZi8HH9Cpajno4pFiu6mQDVTkkyDHTqyo7Bv3IFpdNYiRDAZ1yh1cBOfufMy1gSZQetCwETFxdsOgw7JvKL/gEN+RAFKZF2oUriCsAkYYbxW1cfrqa/YRXUw0ho+n4Jw==",
  "authMode": "MOBILE_OTP / EMAIL_OTP"
}
```
**Responses**

200 Return transaction id in case of success

201 Created

2. Resend Mobile OTP f registration transaction 
 
**URL: https://dev.abdm.gov.in/cm/v1/apps/resend/otp**

**Method**: POST

**HEADERS**: 

**Request body**
```
{
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```
**Responses**

200 Return transaction id in case of success

201 Created

3. Verify the mobile/email OTP to create the PHR ID.

**URL: https://dev.abdm.gov.in/cm/v1/apps/validate/otp**

**Method**: POST

**HEADERS**: 

**Request body**
```
{
  "value": "tSCaVUjHwHiMVCokz7u3ogfop5r7ON5GmVY4rJNaQhoVAMlZl5lDqbb4vobfFMsQ1zO404gkWqPqLoDCdavx+JJ5pxprDpRo+PbeV44q51xr5OoNW2ITy9x6WM81KF9o7OnIU3FOGg09jqcJ/By3S8ICWxzJDKVwCJPehHtjhSFiy+mdWEjKkBTrEWJRTy3ZOkij+fskm+JjLoJlIF0TmA94Jb/avX0/LrnacpWEYWAHd0R/8/HIeITVNwG5hnsuRyIcIKKy7bEuYul8wJDD8RPBhL/gIAV4c5zDCb518o1MJGQtNg8Yf/zcROdaynWrBHIh2tacPrxmLHiZHD+BHQ==",
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Responses**

200 Return Transaction Number in case of success

201 Created

4. Register the beneficiary to the PHR using Mobile/Email address

**URL**: https://dev.abdm.gov.in/cm/v1/apps/registration/details

**Method**: POST

**HEADERS**: 

**Request body**
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
**Responses*

200 Return transaction id in case of success

201 Created

5.  Register the beneficiary to the PHR using Mobile/Email address

**URL**: https://dev.abdm.gov.in/cm/v1/apps/create/phrAddress

**Method**: POST

**HEADERS**: 

**Request body**
```
{
  "alreadyExistedPHR": true,
  "password": "HNceo964MVndrs8Z2oMtzIsmmbzagveHbWkDsDKskTue+/YZhHHrMon19J03ggU457upzWMIX0nU3d38xjB3FxA2qWCVmvLZ98A9l0y3i33vq1ywu9cORGF4OEqV8l7H9h4tDnLGDHnbOh9ct85VfOohP4p73lqW6WQSMYcU+xkBfEsRj42pWL19EVsE1UULtQE8gYY1B0SeM63svUp1kQ4Pt5hdgKxibYBq+hRcck2PkEIhp2N7AkjH4Tf+AhXU9956WLwjKgAKMk7K4+Zv8JtxYCcblQitbpN4ImPH5edf4mO5R/L9RpdAVSllAQQfPIDlp5ZGOZ1GrSmhzOSP3g==",
  "phrAddress": "user@abdm",
  "sessionId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```
**Responses**

200 Return user token id in case of success

201 Created

# Sign-in/Login in PHR App

The PHR mobile application developed by ABDM is now known as ABHA mobile application and has been taken as a reference PHR application. In this application, by login we means login into application using ABHA address aka PHR address, which is an easy to remember PHR address along with its password. 
In the ABHA app which is a reference app, login can be done by four ways:
1. Login via Mobile number
2. Login via ABHA address
3. Login via Email ID
4. Login via ABHA number 

**API Sequence for Login with PHR Address via password /mobile/email otp**

**API Sequence Diagram**
![Sequence](APISequencediagramLoginviapasswordmobileOTP.png)

Swagger link for APIs: https://sandbox.abdm.gov.in/swagger/ndhm-phr-app2.yaml

 1. Get the PHR Address authentication methods.
 **URL: https://dev.abdm.gov.in/cm/v1/apps/phrAddress/search/auth-mode**

**Method**: GET

**Query**: phrAddress-PHR Address

**Responses**
	
200 Return PHR ADDRESS Authentication method Details in case of success

400 Bad request, check request before retrying

2. Initiate the login transaction using the PHR address, based on the auth mode generate mobile/Email OTP to start login transaction

**URL: https://dev.abdm.gov.in/cm/v1/apps/phrAddress/auth-init**

**Method**: POST

**HEADERS**: 

**Request body**
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

**Responses**
	
200 Return transaction id in case of success

201 Created

3. Verify the login transaction, based on the auth mode verify password, Mobile/Email OTP

**URL: https://dev.abdm.gov.in/cm/v1/apps/phrAddress/auth-confirm**

**Method**: POST

**HEADERS**: 

**Request body**
```
{
  "transactionId": "de277b66-00ea-4a4a-a29f-bb9a467960aa",
  "authCode": "2xxWA2g4HeLZsG3NB9/Zx676BIAXZaCHZU3LkrXxV0DSCaT1dQpKsd/Nq6tw6yjSOXiY8vM9GJpZ3gnkBttp47ciwVjM7iIKXKZghjuStDxIabUjEA5OdQZkLdiXp0t185s59tfOnKz1FsJeOPBzhM6qAEbn7EgMZounP3aZrS16FQrWahLNVgrxeVOrfg7HgZcwK+EHTP8q8Z9Ya4sW4sdsM3Aptkb1aBpj8j/G36+n9xNEoWTljfCeHdgpwKzWr2yU72ZLUXSEykA722H8NM8L982HNiLlOnBbmoaijMo50MKFse9pmSlveIQGPl3uz/NtAy+5sKLjtt31AR45sQ==",
  "requesterId": "IN0400XX"
}
```

**Responses**
	
200 Return user Token id in case of success

201 Created

**API Sequence for Login with mobile number/email**

Swagger link for APIs: https://sandbox.abdm.gov.in/swagger/ndhm-phr-app2.yaml

**API Sequence Diagram**
![Sequence](APISequenceDiagramLoginviamobile&email.png)
1. Generate Mobile/Email OTP to start login transaction

**URL: https://dev.abdm.gov.in/cm/v1/apps/login/mobileEmail/auth-init**

**Method**: POST

**HEADERS**: 

**Request body**
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
**Responses**
	
200 Return transaction id in case of success

201 Created

2. Verify Mobile/Email OTP to start login transaction

**URL: https://dev.abdm.gov.in/cm/v1/apps/login/mobileEmail/pre-Verify**

**Method**: POST

**HEADERS**: 

**Request body**
```
{
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "authcode": "tSCaVUjHwHiMVCokz7u3ogfop5r7ON5GmVY4rJNaQhoVAMlZl5lDqbb4vobfFMsQ1zO404gkWqPqLoDCdavx+JJ5pxprDpRo+PbeV44q51xr5OoNW2ITy9x6WM81KF9o7OnIU3FOGg09jqcJ/By3S8ICWxzJDKVwCJPehHtjhSFiy+mdWEjKkBTrEWJRTy3ZOkij+fskm+JjLoJlIF0TmA94Jb/avX0/LrnacpWEYWAHd0R/8/HIeITVNwG5hnsuRyIcIKKy7bEuYul8wJDD8RPBhL/gIAV4c5zDCb518o1MJGQtNg8Yf/zcROdaynWrBHIh2tacPrxmLHiZHD+BHQ==",
  "requesterId": "IN0410XX"
}
```

**Responses**
	
200 Return list of phr address mapped with mobile in case of success

201 Created

3. Get the user token in the mobile/email login flow

**URL: https://dev.abdm.gov.in/cm/v1/apps/login/mobileEmail/auth-confirm**

**Method**: POST

**HEADERS**:

**Request body**
```
{
  "patientId": "user@abdm",
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "requesterId": "IN0401XX"
}
```
**Responses**
	
200 Return list of phr address mapped with mobile in case of success

201 Created

**API Sequence for Login with Health ID**

Swagger link for APIs: https://sandbox.abdm.gov.in/swagger/ndhm-phr-app2.yaml

**API Sequence Diagram**
![Sequence](APISequenceDiagramforLoginwithHealthID.png)
1. Search a user by Health ID number

**URL: https://dev.abdm.gov.in/cm/v1/apps/login/hid/search/auth-mode**

**Request body**
```
{
  "healthIdNumber": "11-1111-1111-1111",
  "yearOfBirth": "1994"
}
```
**Responses**
	
200 Return status as true alone with partail details of Health id number in case of success

201 Created

2. Initiate the login transaction using the Health ID number, based on the auth mode generate OTP to start login transaction

**URL: https://dev.abdm.gov.in/cm/v1/apps/login/hid/auth-init**

**Method**: POST

**HEADERS**:

**Request body**
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
**Responses**

200 Return transaction id in case of success

201 Created

3. Verify Mobile/Email OTP to start login

**URL: https://dev.abdm.gov.in/cm/v1/apps/login/mobileEmail/pre-Verify**

**Method**: POST

**HEADERS**:

**Request body**
```
{
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "authcode": "tSCaVUjHwHiMVCokz7u3ogfop5r7ON5GmVY4rJNaQhoVAMlZl5lDqbb4vobfFMsQ1zO404gkWqPqLoDCdavx+JJ5pxprDpRo+PbeV44q51xr5OoNW2ITy9x6WM81KF9o7OnIU3FOGg09jqcJ/By3S8ICWxzJDKVwCJPehHtjhSFiy+mdWEjKkBTrEWJRTy3ZOkij+fskm+JjLoJlIF0TmA94Jb/avX0/LrnacpWEYWAHd0R/8/HIeITVNwG5hnsuRyIcIKKy7bEuYul8wJDD8RPBhL/gIAV4c5zDCb518o1MJGQtNg8Yf/zcROdaynWrBHIh2tacPrxmLHiZHD+BHQ==",
  "requesterId": "IN0410XX"
}
```

**Responses**
	
200 Return list of phr address mapped with mobile in case of success

201 Created

4. Get the user token in the mobile/email login flow

**URL: https://dev.abdm.gov.in/cm/v1/apps/login/mobileEmail/auth-confirm**

**Method**: POST

**HEADERS**:

**Request body**
```
{
  "patientId": "user@abdm",
  "transactionId": "a825f76b-0696-40f3-864c-5a3a5b389a83",
  "requesterId": "IN0401XX"
}
```
**Responses**
	
200 Return list of phr address mapped with mobile in case of success

201 Created



