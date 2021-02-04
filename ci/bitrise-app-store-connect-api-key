# App Store Connect API key - Bitrise setup

To upload builds from Bitrise to App Store Connect, we need to authenticate the connection between Bitrise and App Store. Preferably this is done using the App Store Connect API key.

The setup has 3 stages:
- [Create the App Store Connect API Key](#Create-the-App-Store-Connect-API-Key)
- [Upload the App Store Connect API key to Bitrise](#Upload-the-App-Store-Connect-API-key-to-Bitrise)
- [Adjust the Bitrise Upload step](#Adjust-the-Bitrise-Upload-step)

## Create the App Store Connect API Key

[https://developer.apple.com/documentation/appstoreconnectapi/creating_api_keys_for_app_store_connect_api](Apple documentation.)

The API key can be created only by the Apple Dev Team Account Holder. You will need to contact this person (probably the client) to do it for you.

To create the API key, go to:
- https://appstoreconnect.apple.com
- Users and Access
- Keys
- App Store Connect API

and create a new API key with Admin privileges. Download and save the key (it is a .p8 file and can be downloaded only once). You will also need the issuer ID from this page. 

<p align="center">
  <img src="../images/ci/08-api-key.png?raw=true" alt="App Store Connect API key"/>
</p> 


## Upload the App Store Connect API key to Bitrise

Go to:
- your app on Bitrise
- Workflow
- Code signing tab

Upload the .p8 file to the Generic File Storage and give it a name that you will later fill in to the Upload step. Also make the file protected so noone can download it.

<p align="center">
  <img src="../images/ci/09-api-key.png?raw=true" alt="Bitrise API key upload"/>
</p> 

## Adjust the Bitrise Upload step

Find the "Deploy to iTunes Connect" step in your workflow.

Set these input vars:
- Bitrise App Developer Connection - off
- API Key URL - the variable name of the .p8 file you uploaded to the Generic File Storage in the previous step
- API Key Issuer ID - can be obtained at App Store Connect at the webpage with the API key (see above)
- Email and Password - remove these. They will cause an error otherwise. 

<p align="center">
  <img src="../images/ci/10-api-key.png?raw=true" alt="Bitrise Upload Step"/>
</p> 

All set and done. 

