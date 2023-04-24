# Nodes iOS app distribution

# 📱

### Overview
The purpose of this document is to describe in detail the process for distributing iOS apps. All projects will follow this set of guidelines, and any deviations will be concidered exceptions and handled on a case-by-case basis. 

### Technologies:
##### Bitrise.io: 

Continuous Integration system that automates the building and deployment process. Developers will configure their project for use with Bitrise and builds will be automatically deployed based on this configuration. Developers will not archive and upload builds locally from their own computer, or using their own accounts. 

##### TestFlight

App distribution for all other purposes. Builds for the Monstarlab QA team that require custom entitlements, as well as *all* external and/or builds for Monstarlab clients will be distributed via TestFlight. Note that this requires clients to have at least one Apple ID logged in on a device with the TestFlight app. 

TestFlight builds can be tested by two groups: internal and external testers. Internal testers can test builds as soon as they are available, but must have their Apple ID added to the App Store Connect team. External testing requires a quick one-time review from Apple before being available. Testers can be invited by e-mail alone and do not need to be invited to the App Store Connect team. 


##### App Store

The live app distribution platform managed by Apple. Builds that have been uploaded to iTunes Connect can be submitted for review by Apple. After review, the app is ready for sale in the store (or pending release if that option is enabled). Only apps that have been approved for release by QA will be submitted for review by Apple. Note that any builds uploaded for TestFlight can be submitted for review, so be very careful that *only* release-tested builds are submitted. 
