# App Store Connect API key - Bitrise setup

To upload builds from Bitrise to App Store Connect, we need to authenticate the connection between Bitrise and App Store. Preferably this is done using the App Store Connect API key.

The setup has 3 stages:
- [1. Create the App Store Connect API Key](#1.-Create-the-App-Store-Connect-API-Key)
- [2. Upload the App Store Connect API key to Bitrise](#2.-Upload-the-App-Store-Connect-API-key-to-Bitrise)
- [3. Adjust the Bitrise Upload step](#3.-Adjust-the-Bitrise-Upload-step)

## 1. Create the App Store Connect API Key

[Apple documentation.](https://developer.apple.com/documentation/appstoreconnectapi/creating_api_keys_for_app_store_connect_api)

The API key can be created only by the Apple Dev Team Account Holder. You will need to contact this person (probably the client) to do it for you.

To create the API key, go to:
- https://appstoreconnect.apple.com
- Users and Access
- Keys
- App Store Connect API

and create a new API key with Admin privileges. Download and save the key (it is a .p8 file and can be downloaded only once). 
❗️DO NOT CHANGE THE FILE NAME, OTHERWISE IT WILL BREAK THE STEP IN THE CI ❗️. The file format should be AuthKey_XXXXXXXX.p8. 

You will also need the issuer ID from this page. 

**Once you have downloaded the key, please send it to Martin Majer at Service Desk or the IT team and tell them to put it in the API key 1password vault - as a Secure note, together with the issuer and key ID.**

<p align="center">
  <img src="../images/ci/08-api-key.png?raw=true" alt="App Store Connect API key"/>
</p> 


## 2. Upload the App Store Connect API key to Bitrise

Go to:
- Your app on Bitrise
- Workflow
- Code signing tab

Upload the .p8 file to the Generic File Storage and give it a name that you will later fill in the Upload step. Also make the file protected so no one can download it.

<p align="center">
  <img src="../images/ci/09-api-key.png?raw=true" alt="Bitrise API key upload"/>
</p> 

## 3. Adjust the Bitrise Upload step

Find the "Deploy to iTunes Connect" step in your Workflow.

Set these input vars:
- Bitrise App Developer Connection - off
- API Key URL - the variable name of the .p8 file you uploaded to the Generic File Storage in the previous step.
- API Key Issuer ID - can be obtained at App Store Connect ona the webpage with the API key (see above).
- Email and Password - remove these. They will probably cause an error otherwise. 

<p align="center">
  <img src="../images/ci/10-api-key.png?raw=true" alt="Bitrise Upload Step"/>
</p> 

All set and done. 
