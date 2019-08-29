# Nodes iOS CI - Guide

## Configuration ⚙️

We have two levels of configuration on [project.yml](./project.yml) file.
In the first level we have the information regarding the whole project and the second level is **Target** specific.

According to the configuration you'll tell the CI to make builds for different targets, extensions and configurations.

#### First level - Project

- **xcodeproj: String** - The name of the xcode project file. ❗️
- **workspace: String** - The name of the xcode workspace file.
- **configuration: String** - Name of the build configuration, e.g. "Staging" or "Release". ❗️
- **ci-version: Number** - **`0.1`**, **`0.2`**, or **`1.0`**. Default is currently **`0.2`**
- **hockey-upload: Bool** - Enables uploads to hockey. This is automatically `true` if testflight uploads are enabled.❗️
- **testflight-upload: Bool** - Enables uploads to testflight.❗️
- **disable-hockey-version-check: Bool** - Disable Hockey version check to avoid errors when build number <= current build number on Hockey. Not required, defaults to `false`
- **slack-channel: String** - The name of the channel to report successful builds to.❗️
- **targets: [String: Target]** - List of target settings.❗️


#### Second level - Target

- **enabled**: **Boolean** - Makes the target available for building.❗️
- **scheme**: **String** - The name of the scheme to build. Usually this is the same as the name of the target.❗️
- **hockey-app-id**: **String** - The app ID used for uploading to hockey.❗️
- **testflight-upload-account**: **String** - The email for the Apple ID used to upload to App Store Connect. Default value depends on CI version: 0.1 and 1.0 use ci@nodes.dk, 0.2 uses ci2@nodes.dk 
- **itc_provider**: **String** - The `ShortName` for the associated AppStore Connect team.
- **team-name**: **String** - Apple Developer team name. This should match the distribution certificate's team name.
- **extensions-bundle-ids**: **[String]** - An array of bundle ID's used in app extension.
- **enable-badge**: **Boolean** - Enables the use of `fastlane badge` for non "Release" configurations.

> ❗️- Mandatory keys

## Template:

*project.yml*

```ruby
# This is the project config file
xcodeproj: "REPLACE_PROJECT_NAME.xcodeproj"
configuration: "Test" # Possible configurations: Debug | Test | Release 
ci-version: 1.0
hockey-upload: true
testflight-upload: false
slack-channel: "REPLACE_SLACK_CHANNEL" # replace with your project's Slack Channel name
targets:
  REPLACE_PROJECT_NAME:
    enabled: true
    scheme: "REPLACE_PROJECT_NAME"
    hockey-app-id:
      Debug: "REPLACE_HOCKEY_DEVELOPMENT"
      Test: "REPLACE_HOCKEY_STAGING"
      Release: "REPLACE_HOCKEY_PRODUCTION"
   

```
