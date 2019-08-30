# Nodes iOS Bitrise - Common issues 🤯

If you run into issues this list of things might help you!
In case you find a new error and fixed it please update this doc to help your colleagues! 🙂

## Issues:

#####  error: No signing certificate "iOS Development" found: No "iOS Development" signing certificate matching team ID "id" with a private key was found

If you see this error using v0.2, Go into your build settings -> Code Signing Identity, and manually select Automatic: iOS Developer or iOS Distribution for your *target* and not the project. This error occurs when the target inherits the code signing identity value from the project.

--

##### Prepare repository fails at checking Hockey version
This happens due to the info plist path in the Xcode project containing a variable, which is usually expanded by Xcode, however, it isn't by the CI script.

Easiest way to fix this issue is by removing the variable part (usually `$(SRCROOT)`) from the info plist path in your target build settings.

--

##### ITC Providers during Testflight upload
If you get this error:
`Your Apple ID account is attached to other iTunes providers. You will need to specify which provider you intend to submit content to by using the -itc_provider command`

For some reason, sometimes the team name isn't enough to tell iTunes Connect which team to upload to. You need to add an extra field like this `itc_provider: "ZLCKLX4ACJ"` to that target in the project.yml file. That value is the Team ID from your account membership page in the developer portal. More info here: https://medium.com/@nickmeehan/fastlane-testflight-and-itc-provider-9233a3c4b5e5

-- 

##### Mutiple teams found

**Note** This one should be solved. If you still get this error, open an issue so we can see what's going wrong


If you see this message when trying to upload to Testflight: `Multiple iTunes Connect Teams found; unable to choose, terminal not ineractive!`

This means fastlane couldn't figure out which team to upload to. The easiest way to fix this is to add an environment variable with either the team name or team id.  In the workflow editor, click Env Vars, and add a new variable under the deploy-testflight workflow. `FASTLANE_ITC_TEAM_ID` = `<team id>`, or `FASTLANE_ITC_TEAM_NAME` = `<team name>`. The team name and ID can be found in logs from the build that failed (there will be a list of teams that it couldn't choose from). Take a look at the fitness DK project for an example of this.

-- 

##### Exit 65 - ARCHIVE FAILED error

Your Xcode archived/build suceeds fine, but CI/fastlane archiving fails with exit code 65? Inspect your Xcode build/archive log for any errors that are outputted - surprisingly Xcode lets you finish the archive while running `xcodebuild` from the commandline (which is what fastlane does) fails horribly.

For example, in one project a `find` command in a custom build phase was outputting an error where it couldn't find a directory.

Search for this error in your Xcode log, if you think something similar to the above might be the cause:
`Command /bin/sh emitted errors but did not return a nonzero exit code to indicate failure`

-- 

##### Codesign error, export failed during Fastlane gym phase

Make sure you remove the translations model generator from your project. It should exist in the project directory but not referenced or linked in the actual xcodeproj.

-- 

##### Loading settings from project.yml

```
+ ruby /var/folders/90/5stft2v13fb_m_gv3c8x9nwc0000gn/T/bitrise034957535/step_src/parse_project_settings.rb
/usr/local/lib/ruby/gems/2.4.0/gems/xcodeproj-1.5.3/lib/xcodeproj/project.rb:217:in `initialize_from_file': [Xcodeproj] Unknown object version. (RuntimeError)
	from /usr/local/lib/ruby/gems/2.4.0/gems/xcodeproj-1.5.3/lib/xcodeproj/project.rb:102:in `open'
	from /var/folders/90/5stft2v13fb_m_gv3c8x9nwc0000gn/T/bitrise034957535/step_src/parse_project_settings.rb:80:in `<main>'
```
We've seen this issue being causes by 2 things:
1. The schemes are not shared
Solution: Share the schemes from xCode -> Product -> Scheme -> Manage schemes -> Make sure "Shared" is checked.
2. The xCode version you are using does not match the stack on the Bitrise project.
Solution: Change the default stack in Bitrise -> Workflow -> Stack
