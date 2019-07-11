# Making manual builds

Sometimes our apps need to be uploaded to hockey manually, usually if there are capabilities enabled for an enterprise-only app. 

## Install HockeyApp for Mac

1. Install HockeyApp from here: https://www.hockeyapp.net/releases/mac/

## Create code-signing files

Fastlane match can handle the code-signing for you. 

1. Set the git_branch if your Matchfile to:

* The client's account name if they are using their own enterprise account
* `nodes-enterprise` if we are using the nodes enterprise account

2. Run `fastlane match enterprise` 

## Set up project signing

1. Disable "Automatically manage signing." 

2. Set the **Signing (Release)** and/or **Signing (Staging)** provisioning profile to the one you just created with fastlane match. It should be `match InHouse <your bundle id>`.  

**Note**: If you need to run debug builds on a device and need code signing, you can either run `fastlane match development` and set the **Signing (Debug)** to that profile, or re-enable "Automatically manage signing"

## Archive and upload

1. Archive your app. Make sure HockeyApp for Mac is open or running. 

2. Do not export the archive! When Xcode is done archiving, you will get a notification from HockeyApp asking if you want to upload your app. 

3. Click upload on the notification, and then upload again in the window that Hockey opens. 

**Note**: If you do not see a notification from Hockey, you can open the HockeyApp client and select "Upload a build" and upload your archive from there. 