---
title: "Setup for Teleconsultation"
date: 2022-05-07T18:00:04+05:30
Weight: 2
draft: false
---


A doctor, after signing in, can select the services they want to provide through the HSPA. There are 3 major steps that a doctor needs to complete before providing any service through UHI

- Set up Calendar/availability
  The doctor can chose to set their available timings on set days. There are two options that can be made available to the doctor
  1. Fixed - The time interval is fixed. 
  2. Flexi - The doctor provides the number of patients they wish to allocate in a hour. Each patient gets a token.
 
- Provide their fees/charges: The doctor can chose to charge different fees for different services they wish to provide. 

## UI Reference
![Reference Screen](../Telecon.png)

## API Sequence
A teleconsultation starts with a /search which is broadcasted to all the registered HSPAs through the gateway. The next set of API calls happen directly with the HSPA and EUA. These include /init and /confirm APIs to which the HSPA responds via /on_init and /on_confirm. 

### Responding to a search request

![Search HSPAs Sequence API](..//Search_HSPAs_SeqAPI.png)

### Example JSONs

The following JSONs represent the Search API that are fired from the EUA for each of the above criteria. If the user provides multiple criteria, the resultant JSON will be a consolidation of the individual parameters used.
The search query is broadcast to all relevant HSPAs by the Gateway and the corresponding on_search callback responses are sent back to the EUA from the Gateway. The on_search response from the HSPA will contain the catalog of doctors who meet the search criteria.
The URL, Method and Headers are the same for all:

> **URL** : {to be added}\
>     **Method**: POST\
> **Headers**: Authorisation 

### a. Doctor's Name
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
                    "name": "Dr. Sana Bhatt"
                }
           }
       }
   }
}
```

### b. Speciality

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
                    "tags": {
                          "@abdm/gov/in/med_speciality" : "Dermatology"
                   }
               }
           }
       }
   }
}
```

### c. System of medicine
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
                    "tags": {
                          "@abdm/gov/in/system_of_med" : "Allopathy"
                   }
                }
           }
       }
   }
}
```

### d. City
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
   }
}
```

### e. Name of hospital/clinic
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
           "provider": {
               "descriptor": {
                    "name": "Victoria Hospital"
                }
           }
       }
   }
}
```
### f. Type of consultation
```
{
   "context": {
       "domain": "uhi:consultation",
       "country": "IND",
       "city": "std:080",
       "action": "search",
       "core_version": "0.7.1",
       "bap_id": "exampleapp.io",
       "bap_uri": "https://api.exampleapp.io/dsep/v0/",
       "message_id": "5ac3dd78-829e-4c7d-9139-a15adbb582cc",
       "timestamp": "2021-03-23T10:00:40.065Z"
   },
   "message": {
       "intent": {
           "fulfillment" : {
               "type" : "Teleconsultation"
           }
       }
   }
}
```
### g. Languages spoken
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
                    "tags": {
                          "@abdm/gov/in/spoken_langs" : [ "hin", "eng" ]
                   }
               }
           }
       }
   }
}
```
### h. Availability (today/this week/this month)

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
               "start": {
                    "time": "2022-05-11T00:00:00.000Z"
               },
               "end": {
                    "time": "2022-05-11T23:59:59.000Z"
               }
           }
       }
   }
}
```
**Response to /search call**
**Status Code: {to be added} (ACK)**

## A sample response via /on_search from one of the HSPAs is as follows:

```
{
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
                  "items": [
                      {
                          "id": "1",
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
                      },
                      {
                          "id": "2",
                          "descriptor": {
                              "name": "Consultation"
                          },
                          "fulfillment_id": "2",
                          "price": {
                              "currency": "INR",
                              "value": "800"
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
                              "name": "Dr Asthana",
                              "gender": "male",
                              "image": "https://image/of/person.png"
                          }
                      },
                      {
                          "id": "2",
                          "type": "PHYSICAL-CONSULT",
                          "agent": {
                              "id": "uhi://hpr?id=6486",
                              "name": "Dr Asthana",
                              "gender": "male",
                              "image": "https://image/of/person.png"
                          },
                          "start": {
                              "location": {
                                  "id": "1",
                                  "gps": "22.343434,77.4534353",
                                  "address": {
                                      "full": "Max Hospitals, Saket, New Delhi, 110021"
                                  }
                              }
                          }
                      },
                      {
                          "id": "1",
                          "type": "DIGITAL-CONSULT",
                          "person": {
                              "id": "uhi://hpr?id=9879",
                              "name": "Dr Sana Bhatt",
                              "gender": "female",
                              "image": "https://image/of/person.png"
                          }
                      },
                      {
                          "id": "2",
                          "type": "PHYSICAL-CONSULT",
                          "person": {
                              "id": "uhi://hpr?id=9879",
                              "name": "Dr Sana Bhatt",
                              "gender": "female",
                              "image": "https://image/of/person.png"
                          },
                          "start": {
                              "location": {
                                  "id": "2",
                                  "gps": "22.343434,77.4534353",
                                  "address": {
                                      "full": "Max Hospitals, Saket, New Delhi, 110021"
                                  }
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

**Response to /on_search call**
  **Status Code: {to be added} (ACK)**

**Postman Collection: {to be added}**


## Displaying search results

### API Sequence
![Display results to the patient](../Display_Results_SeqAPI.png)

### Example JSONs

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

## Book the selected doctor (Initialization of the service)

### ![Book Selected Doctor or Facility](../Book_Selected_SeqAPI.png)

### Example JSONs

The /init API is fired to the HSPA with the selected date and time as well as the customer and billing details. 

> **URL: {to be added}**
> **Method: POST**
> **Headers: Authorisation**

```
{
   "context": {
       "domain": "uhi:consultation",
       "country": "IND",
       "city": "std:080",
       "action": "init",
       "core_version": "0.7.1",
       "bap_id": "exampleapp.io",
       "bap_uri": "https://api.exampleapp.io/uhi/v0/",
       "bpp_id": "examplehspa.io",
       "bpp_uri": "https://api.examplehspa.io/uhi/v0/",
       "message_id": "5ac3dd78-829e-4c7d-9139-a15adbb582cc",
       "timestamp": "2021-03-23T10:00:40.065Z"
   },
   "message": {
       "order": {
           "provider": {
               "id": "facility@hprID",
               "descriptor": {
                   "name": "MAX Hospitals"
               }
           },   
           "item": {
               "id": "1",
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
           },
           "fulfillment": {
               "id": "1",
               "type": "DIGITAL-CONSULT",
               "agent": {
                   "id": "uhi://hpr?id=6486",
                   "name": "Dr. Sana Bhatt",
                   "gender": "Female",
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
               },
               "customer" : {
                   "id" : "john.doe@abdm",
                   "person" : {
                       "name" : "john Doe",
                       "gender" : "male"
                   },
                   "contact" : {
                       "phone" : "+919764718472",
                       "email": "customer@example.com"
                   }
               }
           },
           "billing": {
               "name": "John Doe",
               "address": {
                   "door": "21A",
                   "name": "ABC Apartments",
                   "locality": "Dwarka",
                   "city": "New Delhi",
                   "state": "New Delhi",
                   "country": "India",
                   "area_code": "110011"
               },
               "email": "billed@example.com",
               "phone": "+919876543210"
           }
       }
   }
}
```

> **Response to /init call**\
> **Status Code: {to be added} (ACK)**\
> **Postman Collection: {to be added}**

### A sample response via /on_init from the HSPA is as follows:

```
{
   "context": {
       "domain": "uhi:consultation",
       "country": "IND",
       "city": "std:080",
       "action": "on_init",
       "core_version": "0.7.1",
       "bap_id": "exampleapp.io",
       "bap_uri": "https://api.exampleapp.io/uhi/v0/",
       "bpp_id": "examplehspa.io",
       "bpp_uri": "https://api.examplehspa.io/uhi/v0/",
       "message_id": "5ac3dd78-829e-4c7d-9139-a15adbb582cc",
       "timestamp": "2021-03-23T10:00:40.065Z"
   },
   "message": {
       "order":{
           "provider": {
               "id": "289edce4-d002-4962-b311-4c025e22b4f6",
               "descriptor": {
                   "name": "MAX Hospitals"
               }
           },  
           "item": {
               "id": "1",
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
           },
           "fulfillment": {
               "id": "1",
               "type": "DIGITAL-CONSULT",
               "agent": {
                   "id": "uhi://hpr?id=6486",
                       "name": "Dr. Sana Bhatt",
                       "gender": "Female",
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
               },
               "customer" : {
                   "id" : "john.doe@abdm",
                   "person" : {
                       "name" : "john Doe",
                       "gender" : "male"
                   },
                   "contact" : {
                       "phone" : "+919764718472",
                       "email": "customer@example.com"
                   }
               }
           },
           "billing": {
               "name": "John Doe",
               "address": {
                   "door": "21A",
                   "name": "ABC Apartments",
                   "locality": "Dwarka",
                   "city": "New Delhi",
                   "state": "New Delhi",
                   "country": "India",
                   "area_code": "110011"
               },
               "email": "user@example.com",
               "phone": "+919876543210"
           },
           "quote":{
               "price":{
                   "currency": "INR",
                   "value": "1500"
               },
               "breakup":[
                   {
                       "title": "Consultation",
                       "price": {
                           "value": "1000",
                           "currency": "INR"
                       }
                   },
                   {
                       "title": "CGST @ 5%",
                       "price": {
                           "value": "50",
                           "currency": "INR"
                       }
                   },
                   {
                       "title": "SGST @ 5%",
                       "price": {
                           "value": "50",
                           "currency": "INR"
                       }
                   },  
                   {
                       "title": "Registration",
                       "price": {
                           "value": "400",
                           "currency": "INR"
                       }
                   }
               ]
           },
           "payment": {
               "uri": "https://api.bpp.com/pay?amt=1500&mode=upi&vpa=sana.bhatt@upi",
               "tl_method": "http/get",
               "params": {
                   "amount": "1500",
                   "mode": "upi",
                   "vpa": "sana.bhatt@upi"
               },
               "type": "ON-ORDER",
               "status": "NOT-PAID"
           }
       }
   }
}
```
## Confirm booking

### API Sequence

![Confirm Booking](../Confirm_Booking_SeqAPI.png)

### Example JSONs

he /init API is fired to the HSPA with the selected date and time as well as the customer and billing details. 

> URL: {to be added}
> Method: POST
> Headers: Authorisation 

```
{
   "context": {
       "domain": "uhi:consultation",
       "country": "IND",
       "city": "std:080",
       "action": "confirm",
       "core_version": "0.7.1",
       "bap_id": "exampleapp.io",
       "bap_uri": "https://api.exampleapp.io/uhi/v0/",
       "bpp_id": "examplehspa.io",
       "bpp_uri": "https://api.examplehspa.io/uhi/v0/",
       "message_id": "5ac3dd78-829e-4c7d-9139-a15adbb582cc",
       "transaction_id": "8fa243cd-9f26-4a43-a422-714ba8f41bf2",
       "timestamp": "2021-03-23T10:00:40.065Z"
   },
   "message": {
       "order":{
           "provider": {
               "id": "289edce4-d002-4962-b311-4c025e22b4f6",
               "descriptor": {
                   "name": "MAX Hospitals"
               }
           },  
           "item": {
               "id": "1",
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
           },
           "fulfillment": {
               "id": "1",
               "type": "DIGITAL-CONSULT",
               "agent": {
                   "id": "uhi://hpr?id=6486",
                   "name": "Dr. Sana Bhatt",
                   "gender": "Female",
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
               },
               "customer" : {
                   "id" : "john.doe@abdm",
                   "person" : {
                       "name" : "john Doe",
                       "gender" : "male"
                   },
                   "contact" : {
                       "phone" : "+919764718472",
                       "email": "customer@example.com"
                   }
               }
           },
           "billing": {
               "name": "John Doe",
               "address": {
                   "door": "21A",
                   "name": "ABC Apartments",
                   "locality": "Dwarka",
                   "city": "New Delhi",
                   "state": "New Delhi",
                   "country": "India",
                   "area_code": "110011"
               },
               "email": "user@example.com",
               "phone": "+919876543210"
           },
           "quote":{
               "price":{
                    "currency": "INR",
                    "value": "1500"
                    },
               "breakup":[
                   {
                       "title": "Consultation",
                       "price": {
                           "value": "1000",
                           "currency": "INR"
                       }
                   },
                   {
                       "title": "CGST @ 5%",
                       "price": {
                           "value": "50",
                           "currency": "INR"
                       }
                   },
                   {
                       "title": "SGST @ 5%",
                       "price": {
                           "value": "50",
                           "currency": "INR"
                       }
                   },  
                   {
                       "title": "Registration",
                       "price": {
                           "value": "400",
                           "currency": "INR"
                       }
                   }
               ]
           },
           "payment": {
               "uri": "https://api.bpp.com/pay?amt=1500&txn_id=ksh87yriuro34iyr3p4&mode=upi&vpa=sana.bhatt@upi",
               "tl_method": "http/get",
               "params": {
                   "transaction_id": "abc128-riocn83920",
                   "amount": "1500",
                   "mode": "upi",
                   "vpa": "sana.bhatt@upi"
               },
               "type": "ON-ORDER",
               "status": "PAID"
           }
       }
   }
}
```
> **Response to /init call**\
> **Status Code: {to be added} (ACK)**\
> **Postman Collection: {to be added}**

### A sample response via /on_confirm  from the HSPA is as follows:

```
{
   "context": {
       "domain": "uhi:consultation",
       "country": "IND",
       "city": "std:080",
       "action": "on_confirm",
       "core_version": "0.7.1",
       "bap_id": "exampleapp.io",
       "bap_uri": "https://api.exampleapp.io/uhi/v0/",
       "bpp_id": "examplehspa.io",
       "bpp_uri": "https://api.examplehspa.io/uhi/v0/",
       "message_id": "5ac3dd78-829e-4c7d-9139-a15adbb582cc",
       "transaction_id": "8fa243cd-9f26-4a43-a422-714ba8f41bf2",
       "timestamp": "2021-03-23T10:00:40.065Z"
   },
   "message": {
       "order":{
           "id":"18393748",
           "state":"CONFIRMED",
           "provider": {
               "id": "289edce4-d002-4962-b311-4c025e22b4f6",
               "descriptor": {
                   "name": "MAX Hospitals"
               }
           }, 
           "item": {
               "id": "1",
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
           },
           "fulfillment": {
               "id": "1",
               "type": "DIGITAL-CONSULT",
               "agent": {
                   "id": "uhi://hpr?id=6486",
                   "name": "Dr. Sana Bhatt",
                   "gender": "Female",
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
               },
               "customer" : {
                   "id" : "john.doe@abdm",
                   "person" : {
                       "name" : "john Doe",
                       "gender" : "male"
                   },
                   "contact" : {
                       "phone" : "+919764718472",
                       "email": "customer@example.com"
                   }
               }
           },
           "billing": {
               "name": "John Doe",
               "address": {
                   "door": "21A",
                   "name": "ABC Apartments",
                   "locality": "Dwarka",
                   "city": "New Delhi",
                   "state": "New Delhi",
                   "country": "India",
                   "area_code": "110011"
               },
               "email": "user@example.com",
               "phone": "+919876543210"
           },
           "quote":{
               "price":{
                    "currency": "INR",
                    "value": "1500"
                    },
               "breakup":[
                   {
                       "title": "Consultation",
                       "price": {
                           "value": "1000",
                           "currency": "INR"
                       }
                   },
                   {
                       "title": "CGST @ 5%",
                       "price": {
                           "value": "50",
                           "currency": "INR"
                       }
                   },
                   {
                       "title": "SGST @ 5%",
                       "price": {
                           "value": "50",
                           "currency": "INR"
                       }
                   }, 
                   {
                       "title": "Registration",
                       "price": {
                           "value": "400",
                           "currency": "INR"
                       }
                   }
               ]
           },
           "payment": {
               "uri": "https://api.bpp.com/pay?amt=1500&txn_id=ksh87yriuro34iyr3p4&mode=upi&vpa=sana.bhatt@upi",
               "tl_method": "http/get",
               "params": {
                   "transaction_id": "abc128-riocn83920",
                   "amount": "1500",
                   "mode": "upi",
                   "vpa": "sana.bhatt@upi"
               },
               "type": "ON-ORDER",
               "status": "PAID"
           }
       }
   }
}
```
