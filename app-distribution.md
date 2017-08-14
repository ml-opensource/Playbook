# Nodes iOS app distribution

# 📱

### Overview
The purpose of this document is to describe in detail the process for distributing iOS apps. All projects will follow this set of guidelines, and any deviations will be concidered exceptions and handled on a case-by-case basis. 

### Technologies:
##### Bitrise.io: 

Continuous Integration system that automates the building and deployment process. Developers will configure their project for use with Bitrise and builds will be automatically deployed based on this configuration. Developers will not archive and upload builds locally from their own computer, or using their own accounts. 


##### Hockey app 

App distribution platform for *Nodes QA testing only*. Builds deployed to Hockey will always be signed using our Nodes enterprise distribution profile for fast deployment for QA. This means any custom entitlements (push notifications, universal links, background modes, etc) will not work.

##### TestFlight

App distribution for all other purposes. Builds for the Nodes QA team that require custom entitlements, as well as *all* external and/or builds for Nodes clients will be distributed via TestFlight. Note that this requires clients to have at least one Apple ID logged in on a device with the TestFlight app. 

TestFlight builds can be tested by two groups: internal and external testers. Internal testers can test builds as soon as they are available, but must have their Apple ID added to the iTunes Connect team. External testing requires a quick one-time review from Apple before being available. Testers can be invited by e-mail alone and do not need to be invited to the iTunes Connect team. 


##### App Store

The live app distribution platform managed by Apple. Builds that have been uploaded to iTunes Connect can be submitted for review by Apple. After review, the app is ready for sale in the store (or pending release if that option is enabled). Only apps that have been approved for release by QA will be submitted for review by Apple, and the Nodes AMT team will manage this process. Note that any builds uploaded for TestFlight can be submitted for review, so be very careful that *only* release-tested builds are submitted. 

### Process:

When a developer is ready to deploy an app, they will tag the latest commit, which starts the building and deployment process on Bitrise. A configuration file is used to determine which distribution platforms and which build configuration to use. A standard project has two deployable configurations: Staging and Release (production/live). Each of these configurations can be deployed to Hockey, TestFlight, or both. However, each build can only have one configuration. This means if both a Staging and Release build are required, there will be two builds made (with different version numbers). Also note that this means Staging builds can be uploaded to TestFlight, so it is very important that these builds are not submitted to the App Store. 

When the deployment is finished, a notification will be sent to the appropriate Slack channel. Builds that have been uploaded to Hockey will have a link provided. Uploads to TestFlight will take some time to process before being available to test. Apple sends an automated email response when the build is available for testing by internal testers. 