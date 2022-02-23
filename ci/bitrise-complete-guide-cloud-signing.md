# Monstarlab iOS Bitrise - Setup Guide with Cloud Code Signing 🛠

This is a simple Bitrise app setup guide that makes use of Apple Cloud Code Signing. What this means is that the code signing is managed automatically by Apple. The code signing files are fetched from the Apple servers after the archiving process. You only need to upload the development signing certificate (its .p12 private key file) to the Bitrise app which is needed to create the initial archive.
You also need to make sure that you have the apps, their bundle ids, the production certificate and provisioning profiles (including the entitlements) configured correctly in the App Store Connect. The connection and authentication with Apple is managed using an App Store Connect API key. 

## Features of this setup: 
 - Easy setup in the Bitrise GUI
 - Builds two XCode configurations: Release and Test
 - Uses App Store Connect API key to code sign and send builds to Testflight
 - Deploys builds to Testflight only
 - Builds triggered by commit tags - `*`, `*_release` and `*_test`
 - Sends a success message to Slack - does not send anything on failure
 - Works with CocoaPods and SPM. Carthage is dead ☠️

## Steps: 
- [1. Xcode setup](#Xcode-setup)
- [2. App setup on Bitrise](#App-setup-on-Bitrise)
- [3. Environment vars setup](#Environment-vars-setup)
- [4. Secrets setup](#Secrets-setup)
- [5. Code signing](#Code-signing)
- [6. App Store Connect Authentication](#App-Store-Connect-Authentication)

## Xcode setup

Make sure your project's schemes are ***shared (including app extensions)***. 
Enable ***Automatically manage signing*** for all the configurations you want to build in the CI. If you do not do this, you will get failures in the Archive step. 

<p align="center">
  <img src="../images/ci-cloudSigning/1_1.png?raw=true"/>
</p> 


## App setup on Bitrise

1) Create a new App from the Bitrise dashboard
- Make sure you choose **Monstarlab** account when creating the new app and make it **Private**

<p align="center">
  <img src="../images/ci-cloudSigning/2_1.png"/>
</p> 

2) Connect the repository to Bitrise

<p align="center">
  <img src="../images/ci-cloudSigning/2_2.png"/>
</p> 


3) When setting up the access make sure to add our SSH key using the private key found in the [ci-resources-ios](https://github.com/nodes-projects/ci-resources-ios/blob/master/privatekey) repository.

<p align="center">
  <img src="../images/ci-cloudSigning/2_3.png"/>
</p> 


4) Indicate which branch Bitrise should use to make the builds. Usually develop. 

5) After choosing the branch, Bitrise will validate the source code and then you can select the *export method* you want to use. Go with ***app store***. Bitrise should also autodetect your project file and scheme.

<p align="center">
  <img src="../images/ci-cloudSigning/2_4.png"/>
</p> 

6) The last step is the Webhook setup. This is used to trigger the builds by tags. Tap on **Register a webhook for me**. If the automatic registration does not work, you can [setup the webhook manually](https://devcenter.bitrise.io/en/apps/webhooks/adding-incoming-webhooks.html#adding-incoming-webhooks) now or later. You need to have the admin rights for the Github repository of your app for this though. 

<p align="center">
  <img src="../images/ci-cloudSigning/2_5.png"/>
</p> 

## Environment vars setup
In order to make everything work on Bitrise you'll need to copy the template content from [bitrise.yml](https://github.com/nodes-projects/ci-resources-ios/blob/master/bitrise_cloud_signing.yml) into the Bitrise workflow script.

<p align="center">
  <img src="../images/ci-cloudSigning/3_1.png"/>
</p> 

Go to **Workflow > Env** Vars tab. 
You should see all your environment variables here.
- SLACK_CHANNEL - name of the Slack channel to send a message when the build succeeds
- RELEASE_BUILD_CONFIGURATION and TEST_BUILD_CONFIGURATION - change only if you have different names in your project.
- BITRISE_PROJECT_PATH and BITRISE_SCHEME - change them from placeholders to your project's values. 

Leave the BUILD_CONFIGURATION empty. This is assigned in the preparation steps during building.

<p align="center">
  <img src="../images/ci-cloudSigning/3_2.png"/>
</p> 

## Secrets setup
Go to the **Workflow > Secrets** tab. Add these secrets:
- BUILD_TRIGGER_API_TOKEN - Can be found in the **Code** tab of your app on Bitrise. This is needed to trigger the build workflows.
- SLACK_TOKEN - Used to send notifications after successful builds. The token is universal for the Monstarlab Slack Workspace (I think). Can be found [here](https://github.com/nodes-projects/ci-resources-ios/blob/master/slackToken) or copied from another app on Bitrise. 

<p align="center">
  <img src="../images/ci-cloudSigning/4_1.png"/>
</p> 

<p align="center">
  <img src="../images/ci-cloudSigning/4_2.png"/>
</p> 

## Code signing
You only need to upload the development signing certificate to Bitrise. This is used to create the initial xarchive. All the other signing files are downloaded from Apple servers during the build process. 

1) Download the certificate from the Apple Developer portal.
<p align="center">
  <img src="../images/ci-cloudSigning/5_1.png"/>
</p>

2) The certificate is in a .cer format. You will need the private key .p12 file though that is embedded inside the .cer file.
3) Double click the certificate and install it into your Keychain.
4) Find the cert in your Keychain. Expand it and right tap on the private key. Select ***Export <Certificate name>***. If you do not see the private key, you downloaded a certificate without it. You can either find the person who created the certificate and get the original certificate from them or you can create a new certificate. The full certificate with the private key can be downloaded from the Apple Developer portal only once.
<p align="center">
  <img src="../images/ci-cloudSigning/5_2.png"/>
</p>

5) Create a password for the exported key. You will need to fill it later into Bitrise.
6) In Bitrise, go to **Workflow > Code signing** and upload the certificate. Fill in the password and make it protected by clicking on the three dots and selecting **Make protected**.

  
<p align="center">
  <img src="../images/ci-cloudSigning/5_3.png"/>
</p> 

## App Store Connect API Authentication
ASC API key is used to authenticate with the ASC to fetch code signing files and send the builds to the App Store.

#### 1. Create the App Store Connect API Key

[Apple documentation.](https://developer.apple.com/documentation/appstoreconnectapi/creating_api_keys_for_app_store_connect_api)

The API key authentication can be allowed only by the Apple Dev Team Account Holder. You will need to contact this person (probably the client) to do it for you. Once this kind of authentication is allowed, the account's admins can create the keys themselves.

To create the API key, go to:
- https://appstoreconnect.apple.com
- Users and Access
- Keys
- App Store Connect API

and create a new API key with Admin privileges. Download and save the key (it is a .p8 file and can be downloaded only once). 
❗️DO NOT CHANGE THE FILE NAME, OTHERWISE IT WILL BREAK THE STEP IN THE CI ❗️. The file format should be AuthKey_XXXXXXXX.p8. 

You will also need the issuer ID and the key ID from this page. When you have downloaded the key, please send it to Martin Majer at Service Desk so that it can be securely stored.


#### 2. Upload the App Store Connect API key to Bitrise
Next you need to upload the obtained .p8 key file to the Monstarlab organization on Bitrise and set this connection in your app's Team tab. The key works universally for all apps in one Apple Dev Team and can be therefore reused for multiple apps from the same Apple Dev Team.

You can find a guide to set the API key connection for the app [here](https://devcenter.bitrise.io/en/accounts/connecting-to-services/connecting-to-an-apple-service-with-api-key.html#adding-api-key-authentication-data-on-bitrise). 

# Tadaaa, you are all done 🎉
Before making a build, also make sure you use the right version of XCode in the **Stack** tab.
  
Now tag a commit and push the tag to your repo. This should trigger a build.
  
 If you did everything correctly, the build should succeed. No guarantees though, CI can be a b*tch sometimes 😀.

