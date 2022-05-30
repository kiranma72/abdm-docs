#  SMS Notify2  #
ABDM plans to ensure that users are aware of which health facilities are participating in ABDM. HRPs are expected to notify ABDM whenever a new health record is created using this API.

The expected User flow is given below :

![Deep Linking](../USER FLOW – DEEP LINKING.jpg)

- Patient visits a health facility and registers by providing Name, DoB, Gender and Mobile. Patient does not share any ABHA address with the facility.
- If the Health Facility is participating in ABDM, then it will notify ABDM when there is a new health record for this patient. Only the mobile number and the HIP ID of the facility is notified. Facilities are identified by the facility’s HIPCODE. This can be obtained by registering the facility using the Health Facility Registry and linking the facility to a ABDM approved Health Repository Provider Software.
- ABDM will send an SMS to the user with a deep link.
- The content of the message will be:
```
 Dear Madam/Sir,
   <facility name> is now participating in Ayushman Bharat Digital Mission (ABDM).
    Your report at this facility is now ready. See your record by clicking on
    on phr.abdm.gov.in/uhi/<hipcode>
    
    ABDM,NHA
 ```
Following API must be be used by HRPs for the same -

**Endpoint:**
**/v0.5/patients/sms/notify2**

```
  {
    "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
    "timestamp": "2022-02-08T10:48:02.530Z",
    "notification": {
      "phoneNo": "+91-9999999999",
      "hip": {
        "name": "Max Healthcare",
        "id": "DEMO_TEST_008"
      }
    }
  }  
  ```
**Endpoint:**  
**/v0.5/patients/sms/on-notify**

If the SMS notification is successfully sent to the patient then "status" will be "ACKNOWLEDGED" with no error. If the SMS notification is failed then "status" will be "ERRORED" with error.

```
 {
    "requestId": "5f7a535d-a3fd-416b-b069-c97d021fbacd",
    "timestamp": "2022-02-08T10:56:37.221Z",
    "status": "ACKNOWLEDGED",
    "error": {
      "code": 1000,
      "message": "string"
    },
    "resp": {
      "requestId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    }
  }
```
