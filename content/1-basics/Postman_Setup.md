---
title: "Postman Setup"
date: 2023-03-14T18:00:04+05:30
Weight: 5
draft : false
pre : "<b>1.5 </b>"
---


Postman is one of the most popular software testing tools which is used for API testing. With the help of this tool, developers can easily create, test, share, and document APIs.

{{% notice style="primary" title="Overview " icon="list-alt" %}}
- [Download and install Postman](#download-and-install-postman)
- [Download and import collections](#download-and-import-collections)
- [Download and Import environments variables](#download-and-import-environments-variables) 
- [Verify your access to sandbox](#verify-your-access-to-sandbox-using-postman)
{{% /notice %}}

## Download and install Postman App
Steps to download and install the native Postman application

- **Step-1:** Visit the https://www.postman.com/ website using any web browser and choose your desired platform among Mac, Windows or Linux.
- **Step-2:** Click Download.
- **Step-3:** Now check for the executable file in downloads in your system and run it.
- **Step-4:** Postman Installation Starts. Wait for some time to Complete the Installation of Postman.
- **Step-5:** Signup for Postman Account. In the next window, Signup for a Postman Account.

    NOTE: There are two ways to sign up for a Postman account. One is to create an own Postman account, and the other is to use a Google account. Though Postman allows users to use the tool without logging in, signing up ensures that your collection is saved and can be accessed for later use.
- **Step-6:** Click on Save My Preferences. Select the workspace tools you need and click Save My Preferences
- **Step-5:** Now you will see the Startup Screen.
- **Step-6:** Postman is successfully installed on the system.


## Download and import collections
Using Postman Collections, you can group related API requests or share sets of API requests.

Download ABDM Collections [here](../ABDM_API_postman_collection.json) (ABDM API.postman_collection.json)

We can import Collections in Postman. To perform this task, follow the below steps −

**Step-1:** Select the **Collections** in the left and then click on Import button in the Postman application.
![import button](../import_postman_collection.png)
**Step-2:** Import pop-up shall open with the options to import from a File, Folder, Link, Raw text and Code Repository.
![import menu](../import_menu.png)
**Step-3:** click on choose files and select the Postman collection (ABDM API.postman_collection.json - which was downloaded earlier) to import. 
![import collection](../import_collection.png)
**Step-4:** Click on Import button. The collection would have been imported.
![import menu](../after_collection_import.png)

###### List of collections 
![import menu](../sample_collection_list.png)

## Download and Import environments variables
The Environment variables allow developers to store and reuse parameter values in API requests and scripts. If you need to update a variable value, you can do it in one place and the value will be automatically changed throughout your request collections. The environment variables in Postman can be used in the URLs, in the POST parameters, in the JavaScript code, etc. To specify the variable, use the brackets as a variable name placeholder({{ }}. For example, {{access_token}}).

Download ABDM Environment variables [here](../ABDM.postman_environment.json) (ABDM.postman_environment.json)

**Step-1:** Select the **Environments** in the left and then click on Import button in the Postman application.
![import button](../environment_import.png)
**Step-2:** Import pop-up shall open with the options to import from a File, Folder, Link, Raw text and Code Repository.
**Step-3:** click on choose files and select the Postman environment variables json file (ABDM.postman_environment.json - which was downloaded earlier) to import. 
![import collection](../environment_variables_files_imported.png)
**Step-4:** Click on Import button. The environment variables would have been imported.
![import menu](../after_environment_import.png)

select the downloaded variable from the dropdown in the right to resolve the variables. 
![set environment variable dropdown](../select_environment_variable_dropdown.png)

Now you can see the variables has been resolved
![set environment variable dropdown](../variables_resolved.png)

## Verify your access to sandbox using Postman
