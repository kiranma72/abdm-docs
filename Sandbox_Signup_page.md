# User Manual for Sandbox Sign Up
**Step 1:**  
Start by registering yourself on ABDM Sandbox at the below URL  
https://sandbox.abdm.gov.in/applications/Home/signup_form  
**Step 2:**  
The application will be reviewed by the Sandbox Committee and after review, the Committee will give approval and rejection with remarks.  
_Note_: The committee meets once a week. Hence, please expect 7 days turnaround time.  
https://sandbox.ndhm.gov.in/applications/Home/admin

##### User Activity with new application:
**Step 1:** Signup using the below URL as _Company_ or _Individuals_ per requirement.
 https://sandbox.ndhm.gov.in/applications/Home/signup_form

![HomePage](/uploads/05663334efc59a6007c9202043d629cf/HomePage.png)  

![Fill_Form](/uploads/7bba7a4b751045bb9283f5f7c4aee3fa/Fill_Form.png)

Select appropriate _Entity_, _Type of Application_, _Category_ value.

![License_in_India](/uploads/2d6a3bf46b564a851c75285d9256f8b9/License_in_India.png)

**_Registere/License to operate in India:_** Select _Yes_ if a license is from India otherwise select _No_ then the committee will decide on a case-to-case basis.

![Intent_FOr_Request](/uploads/ade2d2dd3e7e47e97c2c91812d4790fc/Intent_FOr_Request.png)

Currently, try to select the appropriate _Intent For Request_ under which the user wants to register with. In case, an incorrect option is selected, _Don't worry_ the user can change it later.

**Step 2:** Click on Submit Button  

**URL:** https://sandbox.abdm.gov.in/applications/Home/signup_form  
**Method:** POST  
**Request:**  
```sh
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="csrf_name"

d86836039e908f833aa01aaac2f363ad
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="application_type"

3
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="entity"

Company
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="type_of_entity"

Private entity
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="category"

Healthcare Solution Provider
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="res_india"

Yes
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="organisation"

Sandboxtesting
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="gstin"

01VGACL0582H1Z0
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="business"

Testing
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="address"

NA
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="Website"

https://test.com
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="name"

LTITest
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="role"

1
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="email"

Selvaganesh.Tamilarasan@lntinfotech.com
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="mobile"

9952837134
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="password"

Lntinfotech@2022
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="officetype[]"

Health Info Provider
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="echosystem"

TESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTESTTEST
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="Sandboxpolicy"

option2
------WebKitFormBoundaryJjsLx13pa8AWx2Uh
Content-Disposition: form-data; name="submit"

submit
------WebKitFormBoundaryJjsLx13pa8AWx2Uh—
```

**Step 3:** Once the Sandbox request form is submitted, the user can see the application submitted status by login in with _Email id_ and _Password_.  
https://sandbox.ndhm.gov.in/applications/Home/login  

![SandboxLogin](/uploads/d0fdf359069992c0371896324867f785/SandboxLogin.png)  

**Step 4:** On login, _Application Submitted_ status in green color will be displayed and another status in Grey color.  

![Landing_Page](/uploads/074aed6d0a8427ef14dd75a296d75902/Landing_Page.png) 

**Step 5:** Once the application is _Approved_ by the committee, an email will be received by the user stating _Client id_ & _Client Secret_. On Frontend, the user will see the status changed to _Sandbox Application Status_.  

**Step 6:** Once _Client id_ & _Client Secret_ are received via an email, please verify it and check if the correct response is received.  

**URL:** https://dev.abdm.gov.in/gateway/v0.5/sessions  
**Request:** POST  
**Body:**
```sh
{
    "clientId": "string",
    "clientSecret": "string",
    "grantType": "client_credentials"
}
```
**Response:**
```sh
{
  
    "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJBbFJiNVdDbThUbTlFSl9JZk85ejA2ajlvQ3Y1MXBLS0ZrbkdiX1RCdkswIn0.eyJleHAiOjE2NTEwNTA4NzQsImlhdCI6MTY1MTA1MDI3NCwianRpIjoiMDViN2RmNGEtMmFiNS00MjZhLTg2NjMtZGI0YTk5N2YyOWZmIiwiaXNzIjoiaHR0cHM6Ly9kZXYubmRobS5nb3YuaW4vYXV0aC9yZWFsbXMvY2VudHJhbC1yZWdpc3RyeSIsImF1ZCI6ImFjY291bnQiLCJzdWIiOiI4NDgxZjM5MC01MmJjLTRkM2UtOGNjZS1lMjRkODQ1YTIyOTAiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJQUklZQU5LQV9MVEkiLCJzZXNzaW9uX3N0YXRlIjoiODk1M2IzZGItY2RjNC00OTJjLTlkOTctNTJjOWIwZjI4MzE2IiwiYWNyIjoiMSIsImFsbG93ZWQtb3JpZ2lucyI6WyJodHRwOi8vbG9jYWxob3N0OjkwMDciXSwicmVhbG1fYWNjZXNzIjp7InJvbGVzIjpbImhpdSIsIm9mZmxpbmVfYWNjZXNzIiwiaGVhbHRoSWQiLCJPSURDIiwiaGlwIl19LCJyZXNvdXJjZV9hY2Nlc3MiOnsiUFJJWUFOS0FfTFRJIjp7InJvbGVzIjpbInVtYV9wcm90ZWN0aW9uIl19LCJhY2NvdW50Ijp7InJvbGVzIjpbIm1hbmFnZS1hY2NvdW50IiwibWFuYWdlLWFjY291bnQtbGlua3MiLCJ2aWV3LXByb2ZpbGUiXX19LCJzY29wZSI6Im9wZW5pZCBlbWFpbCBwcm9maWxlIiwiY2xpZW50SG9zdCI6IjEwLjIzMy42OS45MyIsImVtYWlsX3ZlcmlmaWVkIjpmYWxzZSwiY2xpZW50SWQiOiJQUklZQU5LQV9MVEkiLCJwcmVmZXJyZWRfdXNlcm5hbWUiOiJzZXJ2aWNlLWFjY291bnQtcHJpeWFua2FfbHRpIiwiY2xpZW50QWRkcmVzcyI6IjEwLjIzMy42OS45MyJ9.SAFsIp5LQzAa8JTMeHQVxXCrWmvbLmho69YzxbtOgdRNkESVEGl3JGUzPfFutEQYyRqj9BCn2xbu0LlT7497-XIRrGVHcL680-TQh-iv_M75elQn9O7kmsvyreKf1HtRboSn3cAqSkMbRNsroYsNjcI0XjRX9J8o5auipbrd9B6ZHL8HYl08bdWLr18FqEulEaLe6poJOyw67_R4hwCtJdqW0uIva9hTbgAGik8J5jcUWhcTg9kasKLugF8XWgc0VbD1krnYC6S7yyBYojYBaN_6N5uQtWPUm2DUUXR1E9uJ1TdILIpAt2Pbe3O4eNV2fyV_FA0HdS3GOCZA_knrhw",
    "expiresIn": 600,
    "refreshExpiresIn": 1800,
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICIyMWU5NzA4OS00ZTcxLTQyNGEtOTAzYS1jOTAyMWM1NmFlNWYifQ.eyJleHAiOjE2NTEwNTIwNzQsImlhdCI6MTY1MTA1MDI3NCwianRpIjoiZDJlZWMyNDAtZDRiMC00OTg5LWFhMWYtNDQ0ZGQwNjk0OWY3IiwiaXNzIjoiaHR0cHM6Ly9kZXYubmRobS5nb3YuaW4vYXV0aC9yZWFsbXMvY2VudHJhbC1yZWdpc3RyeSIsImF1ZCI6Imh0dHBzOi8vZGV2Lm5kaG0uZ292LmluL2F1dGgvcmVhbG1zL2NlbnRyYWwtcmVnaXN0cnkiLCJzdWIiOiI4NDgxZjM5MC01MmJjLTRkM2UtOGNjZS1lMjRkODQ1YTIyOTAiLCJ0eXAiOiJSZWZyZXNoIiwiYXpwIjoiUFJJWUFOS0FfTFRJIiwic2Vzc2lvbl9zdGF0ZSI6Ijg5NTNiM2RiLWNkYzQtNDkyYy05ZDk3LTUyYzliMGYyODMxNiIsInNjb3BlIjoib3BlbmlkIGVtYWlsIHByb2ZpbGUifQ.21__jIYFmHZs4DTxbl8iF9SFstrV9PcaY2Hhf4ADOL4",

    "tokenType": "bearer"
}
```
**Step 7:** To refresh current session, need to generate Refresh Token.  

**URL:** https://dev.abdm.gov.in/gateway/v0.5/sessions  
**Request:** POST  
**Body:**  
```sh
{
  "clientId": "String",
  "clientSecret": "String",
  "grantType": "client_credentials",
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICIyMWU5NzA4OS00ZTcxLTQyNGEtOTAzYS1jOTAyMWM1NmFlNWYifQ.eyJleHAiOjE2NTA5OTc0NDQsImlhdCI6MTY1MDk5NTY0NCwianRpIjoiZDVhZmNlODQtMjUyZS00YzZkLThjNGYtNjNhMmJlZDdlNTI3IiwiaXNzIjoiaHR0cHM6Ly9kZXYubmRobS5nb3YuaW4vYXV0aC9yZWFsbXMvY2VudHJhbC1yZWdpc3RyeSIsImF1ZCI6Imh0dHBzOi8vZGV2Lm5kaG0uZ292LmluL2F1dGgvcmVhbG1zL2NlbnRyYWwtcmVnaXN0cnkiLCJzdWIiOiJiZGFmZDdjYy05ODBjLTQ1MTAtYjk5Ny1mMjRjZWUwZDI0MzAiLCJ0eXAiOiJSZWZyZXNoIiwiYXpwIjoiVkFTQU5USF9MVEkiLCJzZXNzaW9uX3N0YXRlIjoiNzliODgxOTctN2U4MS00MGU1LWI0NDctMDdhMzA3YWI0MDRlIiwic2NvcGUiOiJvcGVuaWQgZW1haWwgcHJvZmlsZSJ9.16IAfZq_lK2aJ3DzGWww477IH6q4egw9BakboPVeqnU"
}  
```
**Response:**  
```sh
{
    "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJBbFJiNVdDbThUbTlFSl9JZk85ejA2ajlvQ3Y1MXBLS0ZrbkdiX1RCdkswIn0.eyJleHAiOjE2NTEwNTA4NzQsImlhdCI6MTY1MTA1MDI3NCwianRpIjoiMDViN2RmNGEtMmFiNS00MjZhLTg2NjMtZGI0YTk5N2YyOWZmIiwiaXNzIjoiaHR0cHM6Ly9kZXYubmRobS5nb3YuaW4vYXV0aC9yZWFsbXMvY2VudHJhbC1yZWdpc3RyeSIsImF1ZCI6ImFjY291bnQiLCJzdWIiOiI4NDgxZjM5MC01MmJjLTRkM2UtOGNjZS1lMjRkODQ1YTIyOTAiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJQUklZQU5LQV9MVEkiLCJzZXNzaW9uX3N0YXRlIjoiODk1M2IzZGItY2RjNC00OTJjLTlkOTctNTJjOWIwZjI4MzE2IiwiYWNyIjoiMSIsImFsbG93ZWQtb3JpZ2lucyI6WyJodHRwOi8vbG9jYWxob3N0OjkwMDciXSwicmVhbG1fYWNjZXNzIjp7InJvbGVzIjpbImhpdSIsIm9mZmxpbmVfYWNjZXNzIiwiaGVhbHRoSWQiLCJPSURDIiwiaGlwIl19LCJyZXNvdXJjZV9hY2Nlc3MiOnsiUFJJWUFOS0FfTFRJIjp7InJvbGVzIjpbInVtYV9wcm90ZWN0aW9uIl19LCJhY2NvdW50Ijp7InJvbGVzIjpbIm1hbmFnZS1hY2NvdW50IiwibWFuYWdlLWFjY291bnQtbGlua3MiLCJ2aWV3LXByb2ZpbGUiXX19LCJzY29wZSI6Im9wZW5pZCBlbWFpbCBwcm9maWxlIiwiY2xpZW50SG9zdCI6IjEwLjIzMy42OS45MyIsImVtYWlsX3ZlcmlmaWVkIjpmYWxzZSwiY2xpZW50SWQiOiJQUklZQU5LQV9MVEkiLCJwcmVmZXJyZWRfdXNlcm5hbWUiOiJzZXJ2aWNlLWFjY291bnQtcHJpeWFua2FfbHRpIiwiY2xpZW50QWRkcmVzcyI6IjEwLjIzMy42OS45MyJ9.SAFsIp5LQzAa8JTMeHQVxXCrWmvbLmho69YzxbtOgdRNkESVEGl3JGUzPfFutEQYyRqj9BCn2xbu0LlT7497-XIRrGVHcL680-TQh-iv_M75elQn9O7kmsvyreKf1HtRboSn3cAqSkMbRNsroYsNjcI0XjRX9J8o5auipbrd9B6ZHL8HYl08bdWLr18FqEulEaLe6poJOyw67_R4hwCtJdqW0uIva9hTbgAGik8J5jcUWhcTg9kasKLugF8XWgc0VbD1krnYC6S7yyBYojYBaN_6N5uQtWPUm2DUUXR1E9uJ1TdILIpAt2Pbe3O4eNV2fyV_FA0HdS3GOCZA_knrhw",

    "expiresIn": 600,

    "refreshExpiresIn": 1800,

    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICIyMWU5NzA4OS00ZTcxLTQyNGEtOTAzYS1jOTAyMWM1NmFlNWYifQ.eyJleHAiOjE2NTEwNTIwNzQsImlhdCI6MTY1MTA1MDI3NCwianRpIjoiZDJlZWMyNDAtZDRiMC00OTg5LWFhMWYtNDQ0ZGQwNjk0OWY3IiwiaXNzIjoiaHR0cHM6Ly9kZXYubmRobS5nb3YuaW4vYXV0aC9yZWFsbXMvY2VudHJhbC1yZWdpc3RyeSIsImF1ZCI6Imh0dHBzOi8vZGV2Lm5kaG0uZ292LmluL2F1dGgvcmVhbG1zL2NlbnRyYWwtcmVnaXN0cnkiLCJzdWIiOiI4NDgxZjM5MC01MmJjLTRkM2UtOGNjZS1lMjRkODQ1YTIyOTAiLCJ0eXAiOiJSZWZyZXNoIiwiYXpwIjoiUFJJWUFOS0FfTFRJIiwic2Vzc2lvbl9zdGF0ZSI6Ijg5NTNiM2RiLWNkYzQtNDkyYy05ZDk3LTUyYzliMGYyODMxNiIsInNjb3BlIjoib3BlbmlkIGVtYWlsIHByb2ZpbGUifQ.21__jIYFmHZs4DTxbl8iF9SFstrV9PcaY2Hhf4ADOL4",

    "tokenType": "bearer"

}  
```

Validitiy of Refresh Token is for 600sec.

**Step 8:** Get certs for JWT Verification  

**URL:** https://dev.abdm.gov.in/gateway/v0.5/certs  
**Request:** GET  
**Response:**  
```sh
{
    "keys": [
        {
            "kid": "AlRb5WCm8Tm9EJ_IfO9z06j9oCv51pKKFknGb_TBvK0",
            "kty": "RSA",
            "alg": "RS256",
            "use": "sig",
            "n": "mgmW7W5ZGF_G5cJevwYi8HiPcI-6qS_psnZxa4v3bkwAkyOoOd8-6ketrOI-ZA2PbRbGnxFfZHiI94rdFXJ4Q9ampscsz9NocTIPMPmWydJ8A50pZaYWyikYDSJiDltq7i3WspPKSOuQHrC5h9dMcCVveX5oeg0tO68Z79gwDlpcxiqDbFaphsqDvx-5XkfwiqvOBaybK6_BCBPuTqWMUEuUklLYXu2X7ESHdVNFMFAjxCcCXUtP7LFdvT3nnFekRmG82QbSQSVe4N5tPH8q0MCxSWWn2c15bDnzOF-dvfRCVPRabCzw0M-utHR9diTrWtq6Koi5buxgwM1rbk0p8Q",
            "e": "AQAB",
            "x5c": [
                "MIICrzCCAZcCBgFy/3WZBjANBgkqhkiG9w0BAQsFADAbMRkwFwYDVQQDDBBjZW50cmFsLXJlZ2lzdHJ5MB4XDTIwMDYyOTA5NDEzNloXDTMwMDYyOTA5NDMxNlowGzEZMBcGA1UEAwwQY2VudHJhbC1yZWdpc3RyeTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAJoJlu1uWRhfxuXCXr8GIvB4j3CPuqkv6bJ2cWuL925MAJMjqDnfPupHraziPmQNj20Wxp8RX2R4iPeK3RVyeEPWpqbHLM/TaHEyDzD5lsnSfAOdKWWmFsopGA0iYg5bau4t1rKTykjrkB6wuYfXTHAlb3l+aHoNLTuvGe/YMA5aXMYqg2xWqYbKg78fuV5H8IqrzgWsmyuvwQgT7k6ljFBLlJJS2F7tl+xEh3VTRTBQI8QnAl1LT+yxXb0955xXpEZhvNkG0kElXuDebTx/KtDAsUllp9nNeWw58zhfnb30QlT0Wmws8NDPrrR0fXYk61rauiqIuW7sYMDNa25NKfECAwEAATANBgkqhkiG9w0BAQsFAAOCAQEACkC3TijrXIgi4vn+l1uL1nfdK6vOIL5UZ6yCjSOq7zYW6b3Qe8j7NrPb9RJC+pbIERyNbB+t9hsa5g1L7lkjCNlUuxfJprsJ9LJKlM5g7dYEA6XPCJ7C6AVlarj72vlWXQvwjnQMO2/CM9/Jp5Hnv2Qwjn7NME2OWM0iblc/TD+DEZK5L5mlWMyuBSQo2o/AcOmfG4MoE5Gm/CaOJ47rSrf+lq83e5+dyKh7uLVAa+5WK8Im5nEs6BLSGyo2KlaV0mW9yCkoRLLbipjH8+rJwkUU6iu7QVjz0peGZzYldya5n35gMWH7Bu4HqFneKNRwwD6w8rGNC+uWtgWejDZ3yQ=="
            ],
            "x5t": "EaMhYGUIvMkp8tvSM3QoaqaF8xM",
            "x5t#S256": "vGer6Pt8AhZn8RlbHhAFksOCcGf3u1UWU7Qq-Doy7ro"
        }
    ]
}  
```

