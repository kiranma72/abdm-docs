---
title: "Working with ABDM APIs"
date: 2022-05-07T18:00:04+05:30
Weight: 4
draft: false
---

### How ABDM registers and identifies an entity

Every organization that registers with ABDM is issued one or more Client IDs 

Each Client ID should be used by the organization to register ONE INSTANCE of their ABDM compiliant software

Each instance of the software can hold health records for one or more health facilities 

The figure below explains this using e-Hospital as an example 

![adbm-gw-registry](/abdm-docs/img/abdm-gateway-registry.png)

### The Authorization Header

Almost all ABDM APIs require you to pass the session token obtained via your client ID / secret in the Authorization HTTP Header. Remember to add the word "Bearer " in front of the JWT access Token you obtain from the https://dev.abdm.gov.in/gateway/v0.5/sessions

```

Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6IC.....

```



### ABDM Client IDs and Call back URLs 

HRPs and PHR apps that integrate with the HIE-CM do so via the ABDM gateway. 

The HIE-CM APIs are designed to be asyncronous. When you call an API on the gateway, if the request is accepted you will merely get a HTTP 200 response acknowledging that the request has been recorded. Once the response is available, the gateway is will invoke the callback URL registered for the Client ID

All integrators developing either a HRP or a PHR app must register a call back URL for their Client ID

![Async Arch](/abdm-docs/img/async-callbacks.png)

### Registering your callback URL 

```
curl --location --request PATCH 'https://dev.abdm.gov.in/devservice/v1/bridges' --header 'Content-Type: application/json' --header 'Authorization: Bearer your-access-token-from-gateway-session' --data-raw '{
	"url": "https://my-emr-site.in"
}
```

### Linking the HIPs / HIUs for a Client ID

The HIP code used by ABDM is the same as the health facility registry ID. For details on how to register a health facility that uses your software go (here). 

The API below is only available in the Sandbox for quick setups. You can use it to link ONE HIP / HIU ID with your Client ID with no validations.  

Example
> 
> unique-hip-id: HIP5234127
>
> Your-facility-name: My Nursing Home
>

``` 
curl --location --request PUT 'https://dev.abdm.gov.in/devservice/v1/bridges/services' --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Bearer your-access-token-from-gateway-session' --data-raw '{"id":"unique-hip-id","name":"Your-facility-name","type":"HIP","active":true,"alias":["EG"]}'

```

All HIUs including PHR apps also need to register a HIU code. 
Example
> 
> unique-hiu-id: MyAppName
>
> Your-App-Name: My App Name
>

``` 
curl --location --request PUT 'https://dev.abdm.gov.in/devservice/v1/bridges/services' --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Bearer your-access-token-from-gateway-session' --data-raw '{"id":"unique-hiu-id","name":"Your-App-name","type":"HIU","active":true,"alias":["EG"]}'

```

For detailed APIs related to registration with the ABDM gateway 

> https://sandbox.abdm.gov.in/swagger/ndhm-devservice.yaml


You can quickly try out how async APIs work using webhook

1. Go to https://webhook.site 
2. Copy your unique URL shown on the page 
3. Register it with ABDM Gateway as shown in Registering your callback URL. Ensure you get a Response: 200 
4. Register a HIP / HIU of your choice with your client id as above. Ensure you get a Response: 200 
4. Call a async Gateway API using a @sbx PHR address (if you need a phraddress create it at https://phrsbx.abdm.gov.in)
5. Verify you get a callback at your webhook site. It should look like the image below

![webhook-site](/abdm-docs/img/webhook-site-demo.png) 


### ABDM HTTP Headers

A single ABDM Client (also called a Bridge) can support multiple HIPs / HIUs on the same registered URL. In order to clearly identify which HIP / HIU this message was intented to be sent, the Gateway adds the following headers as part its API calls

1. The X-HIP-ID Header -- Contains the health facility registry code that is linked to the Client ID
2. The X-HIU-ID Header -- Contains the health information user code that is linked to this Client ID

The ABDM architecture is designed to support multiple HIE-CMs. Whenever you call any Gateway API you must include a header that tells the gateway which HIE-CM must this request be sent to 

1. X-CM-ID -- Pass 'sbx' if you are in the sandbox, Pass 'abdm' if you are in production. You must get this from HIE-CM domain name suffixed after the @ symbol in a PHR address. 

### Check your configuration 

**URL:** https://dev.abdm.gov.in/gateway/v1/bridges/getServices

**HEADER:** 
- Authorization : JWT session token

**Response** 
200

```json
{
    "bridge": {
        "id": "TEST_002",
        "name": "Sandbox Test Bridge",
        "url": "https://webhook.site/6ea28791-96fd-4c60-a6ce-a1eb67556370",
        "active": true,
        "blocklisted": false
    },
    "services": [
        {
            "id": "KT-HIU",
            "name": "HIU for KT",
            "types": [
                "HIU"
            ],
            "endpoints": {},
            "active": true
        },
        {
            "id": "KT-HIP",
            "name": "HIP for KT",
            "types": [
                "HIP"
            ],
            "endpoints": {},
            "active": true
        },
    ]
}
```


### Request IDs and Correlation IDs

### Timestamp format 

### Encrypting data feilds 

Several APIs have enhanced security measures and you will need to encrypt the content of some fields.

i. Sensitive data(Data like OTP, Aadhaar Number, Password, Username etc) have to be encrypted.
ii. Data is encrypted by the public certificate. The certificate can be downloaded from the /v2/auth/cert API under Authentication tag in the version 2.
iii. RSA Encryption to encrypt the data. Cipher Type - RSA/ECB/PKCS1Padding. 

Checkout this (online tool)[https://www.devglan.com/online-tools/rsa-encryption-decryption] for data encryption

### Securing your callbacks 


