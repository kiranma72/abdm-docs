---
title: "Delete via Mobile Otp"
date: 2022-05-07T18:00:04+05:30
weight: 1
draft: false
---

## Delete ABHA via Mobile Otp

## Overview of the functionality 

- Users may delete his/her ABHA (Health ID) permanently.

Following will happen if you delete your ABHA (Health ID) :
1. Your ABHA (Health ID) will be permanently deleted, along with all your demographic details .
2. You will not be able to retrieve any information tagged to your ABHA (Health ID) in future.
3. You will never be able to access ABDM applications or any health records over the ABDM network with your deleted ABHA (Health ID).


## API Sequence 

The sequence of APIs used via this method is shown in the diagram below.

![Delete ABHA via Aadhaar Otp](/abdm-docs/img/Delete_ABHA(Health_ID).png)


## API Information Request Response 

1. Generate Mobile OTP to start mobile txn.

Explanation - Api Accepts Auth Token and Generates OTP on mobile number.

Request Body - Required

Responce - Api Accepts Auth Token and Generates OTP on mobile number. Returns Error for Unauthorized token .

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/mobile/generateOTP

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

```json

```

**Response:** 200

```json
{
  "mobileNumber": "XXXXXX2125",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```


2. Delete the account using Mobile otp.

**URL:** https://healthidsbx.abdm.gov.in/api/v2/account/profile/delete

**Request:** POST  

**Parameters:**

- Authorization string (header)

- X-HIP-ID string (header)

- X-Token string (header)


**Body:**

deleteAccountByOtpWebRequest  (body)

```json
{
  "authMethod": "AADHAAR_OTP",
  "otp": "sw1uD+gpv3fj6NHBNhtcII3GksVtkLT9bvcz0svYDyUt/x3jTtedXSYgw4b90GTwfLfs1eow056VsOw9HFS/wB8uH5Ysx+QzpL7PxmAY1WOHwOj04sPKN6Dw8XY8vcXovtvZc1dUB+TPAlGGPNu8iqMVPetukysjRxgbNdLLKMxn46rIRb8NieeyuDx1EHa90jJP9KwKGZdsLr08BysrmMJExzTO9FT93CzoNg50/nxzaQgmkBSbu9D8DxJm7XrLzWSUB05YCknHbokm4iXwyYBsrmfFDE/xCDfzYPhYyhtEmOi4J/GMp+lO+gAHQFQtxkIADhoSR8WXGcAbCUj7uTjFsBU/tc+RtvSotso4FXy8v+Ylzj28jbFTmmOWyAwYi9pThQjXnmRnq43dVdd5OXmxIII6SXs0JzoFvKwSk7VxhuLIRYzKqrkfcnWMrrmRgE8xZ6ZLft6O3IeiHb9WA8b/6/qO8Hdd17FKsSF6te59gSpoajS0FtQIgFn/c+NHzQYo5ZdsuRGM9v+bhHTInI=",
  "password": "string",
  "reactivationDate": "12/2/2021",
  "reasons": "Official requirement",
  "txnId": "a825f76b-0696-40f3-864c-5a3a5b389a83"
}
```

**Response:** 204




## Postman + Curl Collection 

**Download the Postman Collection** [here](/abdm-docs/Postman/)

**Download the Curls** [here](/abdm-docs/Curls/)




