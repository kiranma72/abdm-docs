---
title: "Search HSPAs for Doctor"
date: 2022-05-07T18:00:04+05:30
Weight: 1
draft: false
---


The user can search for a doctor using one or multiple criteria. The supported criteria include
- Doctor name/HPID
- Specialities
- System of medicine
- City
- Hospital/facility
- Availability 
- Type of consultation
- A search can also be completed by a patient browsing their appointment history
- The EUA fires Search API onto the HSPAs to look for the doctors matching the search criteria across the network.

## UI Reference
![Search HSPAs UI Reference](..//Search_HSPAs_UIR.png)


## API Sequence

![Search HSPAs Sequence API](..//Search_HSPAs_SeqAPI.png)

## Example JSONs

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


