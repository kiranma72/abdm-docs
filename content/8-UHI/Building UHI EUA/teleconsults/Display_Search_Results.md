---
title: "Display Search Results"
date: 2022-05-07T18:00:04+05:30
Weight: 2
draft: false
---

# Display search results

- The HSPAs respond with on_search API to send back the HPID of the doctors who match the search criteria of EUA.
- The EUA looks up the Health Professionals Registry (HPR) to fetch the details of the doctor against the HPIDs received from the HSPA.
- The other details such as the quote and availability are fetched by the EUA from the HSPA directly by firing the search API again to the HSPA with the specific doctor’s HPID.
- The EUA collates the results and presents it to the user. 

## Reference UI
![Display results to the patient](../Display_Results_UIR.png)

## API Sequence
![Display results to the patient](../Display_Results_SeqAPI.png)

## Example JSONs
The /search API is fired once again with the specific doctor’s HPR ID to retrieve the doctor’s appointment calendar. This call is made directly to the the HSPA

> URL: {to be added}\
> Method: POST\
> Headers: Authorisation **

- ### Doctor's HPR ID
```
{
   "context": {
       "domain": "uhi:consultation",
       "country": "IND",
       "city": "std:080",
       "action": "search",
       "core_version": "0.7.1",
       "bap_id": "exampleapp.io",
       "bap_uri": "https://api.exampleapp.io/uhi/v0/",
       "message_id": "5ac3dd78-829e-4c7d-9139-a15adbb582cc",
       "timestamp": "2021-03-23T10:00:40.065Z"
   },
   "message": {
       "intent": {
           "fulfillment": {
               "agent": {
                    "id": "<HPR_ID>"
                }
           }
       }
   }
}
```
> **Response to /search call**\
>  **Status Code: {to be added}**\
> **Postman Collection: {to be added}**

### A sample response via /on_search from one of the HSPAs is as follows:
```
"items": [
                       {
                           "id": "1",{
   "context": {
       "domain": "uhi:consultation",
       "country": "IND",
       "city": "std:080",
       "action": "on_search",
       "core_version": "0.7.1",
       "bap_id": "exampleapp.io",
       "bap_uri": "https://api.exampleapp.io/uhi/v0/",
       "bpp_id": "examplehspa.io",
       "bpp_uri": "https://api.examplehspa.io/uhi/v0/",
       "message_id": "85a422c4-2867-4d72-b5f5-d31588e2f7c5",
       "timestamp": "2021-03-23T10:00:40.065Z"
   },
   "message": {
       "catalog": {
           "descriptor": {
               "name": "Example HSPA"
           },
           "providers": [
               {
                   "id": "289edce4-d002-4962-b311-4c025e22b4f6",
                   "descriptor": {
                       "name": "MAX Hospitals"
                   },
                   "locations": [
                       {
                           "id": "1",
                           "gps": "22.343434,77.4534353",
                           "address": {
                               "full": "Max Hospitals, Saket, New Delhi, 110021"
                           }
                       },
                       {
                           "id": "2",
                           "gps": "22.231231,77.987987",
                           "address": {
                               "full": "Max Hospitals, Green Park, New Delhi, 110034"
                           }
                       }
                   ],
 
                           "descriptor": {
                               "name": "Consultation"
                           },
                           "fulfillment_id": "1",
                           "price": {
                               "currency": "INR",
                               "value": "1000"
                           },
                           "quantity": {
                               "available": "1"
                           }
                       }
                   ],
                   "fulfillments": [
                       {
                           "id": "1",
                           "type": "DIGITAL-CONSULT",
                           "agent": {
                               "id": "uhi://hpr?id=6486",
                               "name": "Dr Sana Bhatt",
                               "gender": "female",
                               "image": "https://image/of/person.png"
                           },
                           "start": {
                               "time": {
                                   "timestamp": "2022-04-20T12:00:00Z+5:30"
                               }
                           },
                           "end": {
                               "time": {
                                   "timestamp": "2022-04-20T12:30:00Z+5:30"
                               }
                           }
                       },
                       {
                           "id": "1",
                           "type": "DIGITAL-CONSULT",
                           "agent": {
                               "id": "uhi://hpr?id=6486",
                               "name": "Dr Sana Bhatt",
                               "gender": "male",
                               "image": "https://image/of/person.png"
                           },
                           "start": {
                               "time": {
                                   "timestamp": "2022-04-20T13:00:00Z+5:30"
                               }
                           },
                           "end": {
                               "time": {
                                   "timestamp": "2022-04-20T13:30:00Z+5:30"
                               }
                           }
                       },
                       {
                           "id": "1",
                           "type": "DIGITAL-CONSULT",
                           "person": {
                               "id": "uhi://hpr?id=6486",
                               "name": "Dr Sana Bhatt",
                               "gender": "female",
                               "image": "https://image/of/person.png"
                           },
                           "start": {
                               "time": {
                                   "timestamp": "2022-04-20T14:00:00Z+5:30"
            
                   }
                           },
                           "end": {
                               "time": {
                                   "timestamp": "2022-04-20T14:30:00Z+5:30"
                               }
                           }
                       },
                       {
                           "id": "1",
                           "type": "DIGITAL-CONSULT",
                           "person": {
                               "id": "uhi://hpr?id=6486",
                               "name": "Dr Sana Bhatt",
                               "gender": "female",
                               "image": "https://image/of/person.png"
                           },
                           "start": {
                               "time": {
                                   "timestamp": "2022-04-20T15:00:00Z+5:30"
                               }
                           },
                           "end": {
                               "time": {
                                   "timestamp": "2022-04-20T15:30:00Z+5:30"
                               }
                           }
                       }
                   ]
               }
           ]
       }
   }
}
```
> **Response to /on_search call**\
>  **Status Code: {to be added} (ACK)**\
> **Postman Collection: {to be added}**


