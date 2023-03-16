---
title: "Postman Setup"
date: 2023-03-14T18:00:04+05:30
Weight: 5
draft : false
pre : "<b>1.5 </b>"
---


Postman is one of the most popular software testing tools which is used for API testing. With the help of this tool, developers can easily create, test, share, and document APIs.

{{% notice style="primary" title="Overview " icon="list-alt" %}}
- [Download And Install Postman](#download-and-install-postman-app)
- [Download Collections and Environment Variables](#download-collections-and-environment-variables)
- [Import Collections](#import-collections)
- [Import Environments Variables](#import-environments-variables) 
- [Verify Your Access To Sandbox](#verify-your-access-to-sandbox-using-postman)
{{% /notice %}}

## Download And Install Postman App
Steps to download and install the native Postman application

- **Step-1:** Visit the https://www.postman.com/ website using any web browser and choose your desired platform among Mac, Windows or Linux.
- **Step-2:** Click Download.
- **Step-3:** Now check for the executable file in downloads in your system and run it.
- **Step-4:** Postman Installation Starts. Wait for some time to Complete the Installation of Postman.
- **Step-5:** Startup screen will have "Create an account or sign in"
- **Step-6:** Create Account for Postman Account(If you already don't have an account).

    NOTE: There are two ways to sign up for a Postman account. One is to create the Postman account, and the other is to use a Google account. Though Postman allows users to use the tool without logging in, signing up ensures that your collection is saved and can be accessed for later use.
- **Step-7:** After signing in,in the Postman interface click on *Workspaces* dropdown on the top left. Click on *Create Workspace* button. Enter the name and select the visibility of the workspace and click *Create Workspace*.
- **Step-8:** Now you have the workspace created to enable you to organize your Postman work.

## Download Collections And Environment Variables 

Download API Collection And Environment Variables and extract the files from zip.
[{{% icon icon="download" %}}](../Postman_Collection_And_EnvironmentVariables.zip "download"). 

## Import Collections
Using Postman Collections, you can group related API requests or share sets of API requests.

We can import Collections in Postman. To perform this task, follow the below steps −

- **Step-1:** Select the **Collections** in the left and then click on Import button in the Postman application.
![import button](../import_postman_collection.png)
- **Step-2:** Import pop-up shall open with the options to import from a File, Folder, Link, Raw text and Code Repository.
![import menu](../import_menu.png)
- **Step-3:** click on choose files and select the Postman collection (ABDM_API_postman_collection.json - which was downloaded earlier) to import. 
![import collection](../import_collection.png)
- **Step-4:** Click on Import button. The collection would have been imported.
![after collection import](../after_collection_import.png)

###### Sample List of collections 
![collection list](../sample_collection_list.png)

## Import Environments Variables
The Environment variables allow developers to store and reuse parameter values in API requests and scripts. If you need to update a variable value, you can do it in one place and the value will be automatically changed throughout your request collections. The environment variables in Postman can be used in the URLs, in the POST parameters, in the JavaScript code, etc. To specify the variable, use the brackets as a variable name placeholder({{ }}. For example, {{access_token}}).


- **Step-1:** Select the **Environments** in the left and then click on Import button in the Postman application.
![environment import button](../environment_import.png)
- **Step-2:** Import pop-up shall open with the options to import from a File, Folder, Link, Raw text and Code Repository.
- **Step-3:** click on choose files and select the Postman environment variables json file (ABDM_API_postman_environments.json - which was downloaded earlier) to import. 
![import environment variables](../environment_variables_files_imported.png)
- **Step-4:** Click on Import button. The environment variables would have been imported.
![after environment import](../after_environment_import.png)

select the downloaded variable from the dropdown in the right to resolve the variables. 
![set environment variable dropdown](../select_environment_variable_dropdown.png)

Now you can see the used variables been resolved.
![environment variable resolved](../variables_resolved.png)

## Verify Your Access To Sandbox Using Postman
- **Step-1:** Enter the client Id and client secret in the body of  Gateway Token api which has the **v0.5/sessions** endpoint 
![sessions api](../sessions_api.png)
- **Step-2:** Now click the *Send* button to see the access Token as part of the response below
![sessions api response](../sessions_api_response.png)


