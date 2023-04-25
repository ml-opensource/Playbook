This document is meant for developers. It shows how we work at Monstarlab (IM). 

# Monstarlab (IM) iOS


We love what we do and care about the products we create. They are a team effort, together with our designers, backend developers, project managers, and all the other people at Monstarlab. 

We try to write clean code and separate the pieces of code that occur often in our apps into separate libraries that can be reused in other projects. Our open source activity can be found on [GitHub](https://github.com/nodes-ios).

We try to increase our contribution to the iOS developer community through:

- abstracting relevant parts of our code and turning them into open source libraries that other developers can use
- encouraging our team members to join iOS related meetups, groups and conferences
- encouraging our team members to speak at iOS events
- contributing back to some of the other open source libraries we use through issues and PRs
- encouraging our team members to write tech articles about any topic they desire on our [engineering blog](https://engineering.nodesagency.com/); if needed, we can also suggest topics for new articles

We create lots of apps for our clients. We strive to keep all our applications architecture as modern, consistent and familiar to all developers as possible. We should build all new projects using our [iOS project template](https://github.com/nodes-ios/ios-template), making use of the [Modular MVVM pattern](./ModularArchitecture.md) using SwiftUI & SPM. We should assure all code is tested to a high level where possible. 

# Team meetings
Here are the recurring meetings the iOS team takes part in:

#### iOS Team Meeting
This is the main meeting in the iOS team, where we talk about the latest things happening in our team. The programme normally consists of assessing the general direction of the team, quick updates from each member of the team what they are working on, test of the day (where someone presents a test they have written in the past two weeks) & somebody presenting an approach or some work they have done. It gives the team an opportunity to discuss work and approaches so we can all learn from one another and improve our ways of working. This happens bi-weekly every Thursday morning. 

#### Monthly CTO Update

Each month there will be an update from the CTO Office covering regional status' from APAC, EMEA and AMER as well as progress updates on initiatives being run by the CTO office.


# Your First Day

The IT department is responsible for setting up accounts and giving you access to the tools you need to do your job. The easiest way to contact the IT department is via [Zendesk](https://monstarlab-internal.zendesk.com/hc/en-us).

- Meet with the Head of iOS & your Team Manager. They will be your first persons of reference in the company. Use them as much as you need to get settled in, but also be considerate of their own time.
- Join [our private git](https://github.com/nodes-projects). Ask IT if you don't have access.
- Get the cert sign request and private key from [this private repo here](https://github.com/nodes-projects/keyring-ios). Add the private key to your Keychain and from now on, always use this certificate signing request when creating new certificates on the developer portal. 
- Install the latest Xcode. Ideally, from the [Apple developer portal](https://developer.apple.com/download/more/) and not from the App Store. If you got it from the App Store, that's ok too.
- Get another iOS developer to invite you to our developer accounts.
- We want you to help us make great open source software. So get another iOS developer to invite you to  [our GitHub organisation](https://github.com/nodes-ios). Make sure you enable your 2FA on GitHub. Our client projects are on [our private git](https://github.com/nodes-projects) and our public ones are on [GitHub](https://github.com/nodes-ios).
- Set up your git keys properly, so you can pull and push from both git servers.
- You should have been invited to our Slack and JIRA accounts. Ask IT if you don't have access.
- Make sure to read the [IM Technology Confluence](https://monstarlab.atlassian.net/wiki/spaces/CTO/overview). That is will provide some extra information regarding each practices covered in Monstarlab IM.

# Tools We Use

For employee management, we use [BambooHR](https://nodesagency.bamboohr.com/home). Ask IT if you don't have access and the Chief People Officer if anything in there is unclear. Use this to request time off, register sick day and manage your personal info and banking info for salary payments.

Our main communication tool is [**Slack**](https://nodes.slack.com). We use this for daily communication.

Our main project management tool is [**JIRA**](https://nodesagency.atlassian.net/jira/). Each project has its own JIRA board. Always keep your project's JIRA board up to date to reflect the current status of the project. We work in an agile manner and move fast, but the JIRA board must clearly reflect the project's status. Ask your project manager if you have questions.

With the same JIRA account, you will also have access to Confluence, where you can find project-related documentation, and also internal documents.

[**MPlanner**](https://nplanner.io/) is the tool we use to manage allocation, time tracking and project finance. You can use it to see which project you are assigned to and also track your hours spent on the project. Make sure to always track your time on the appropriate project. Ask the PM on which project you should track. We expect you to track 7.5 hours per day (8 in Germany). Lunchtime is not tracked, and it doesn't count towards the daily work hours.

Use MPlanner to see what project you're assigned to that day. You can also see what other people are assigned to, how long a project should take, when other people are on vacation, etc. Project managers also use MPlanner to see if a project goes over budget (more hours were tracked than allocated). But that's not something you as a developer should care about.

[**Postman**](https://www.getpostman.com/) is a great tool which helps you see and test web APIs. Our backend team uses Postman to test and document their APIs, so all the web APIs for our apps can be found in Postman. You can use it to see the different endpoints available, read their documentation or make requests to those endpoints. Ask IT if you don't have access.

To ease the collaboration between designers and developers, we use [**Figma**](https://www.figma.com/). In Figma, you can see each screen in the design, get info about the sizes, padding, fonts, colours and also export assets for the mobile devices. You can also add notes in Zeplin and communicate with your designer directly on the project.

[**Charles**](https://www.charlesproxy.com/) is an HTTP proxy. You can set your phone / simulator to proxy through Charles and you can see all the API calls it made, you can inspect its requests or responses. It comes in very handy especially if you work with an external, poorly documented API. Ask IT if you need a license.

For in-house distribution and crash reporting, we use [**Firebase**](firebase.google.com/). Depending on the project, sometimes we only use TestFlight. Talk to your PM or with previous developers on that project.

Modern apps should use SPM where possible to manage all dependencies. Older projects may use Carthage or CocoaPods but we should try to use SPM if possible as we believe it is the easiest to use, maintain and manage.

The way we do localization in Monstarlab(IM) is a bit different than in other places. We use [**NStack**](https://nstack.io/), a service we built, which together with the [**NStack SDK**](https://github.com/nstack-io/nstack-ios-sdk) offers dynamic localization for our apps. Go to [nstack.io](https://nstack.io/), log in with your Nodes account, select the app you need (or create a new one), go to "Localize" and add new translations or edit the current ones. A translation consists of a key (by which the string is recognized through the SDK) and one or more values (depending on the number of languages your app is translated to). The translations can be changed in NStack and the changes will reflect in the app without the need for an app update.


# Coding Guidelines
Make sure to read our [**Swift Style Guide**](styleguide.md).  
We use [**Conventional commits**](https://www.conventionalcommits.org/en/v1.0.0) in our commit messages. Mostly `fix:` and `feat:` but feel free to use others as well. These are used to extract change logs.

# Continuous Integration (CI)

As a digital agency, we build hundreds of apps during the day and to manage all these builds we are using Bitrise as a CI tool to speed up our deployment process. The most modern way to setup CI and signing is using cloud signing.

Please refer to our CI setup guide [here](https://github.com/nodes-ios/Playbook/blob/master/ci/bitrise-complete-guide-cloud-signing.md#app-store-setup).

We use SonarQube to monitor code quality. We should run Bitrise on PullRequests, that runs and asserts all tests pass and reports code coverage to SonarQube. For more information on how to setup SonarQube with your Bitrise project, see [here](https://monstarlab.atlassian.net/wiki/spaces/CTO/pages/7591755784/SonarQube+Setup).

***Troubleshooting***
We also listed the most common issues when Bitrise is trying to make the builds. Please check the [common issues document](./ci/bitrise-issues-readme.md) if you are having some problems.


# Working with Remote Colleagues

We are often required to work in teams remotely. Communication is key, more so than ever when this is the case. Our main means of communication inside the company is Slack. Make sure to rely as much as possible on JIRA. 

It helps a lot to try and change your mindset from synchronous communication to asynchronous communication. This means that you try to foresee any problems you might run into and ask about info for them before you actually run into them. Try not to get into a situation where you need an answer from someone to be able to continue.

Always have a good overview of what's left to be done and what you need in order to get it done. 

If you need something (an image asset, some input from the PM, etc), make a JIRA card asking for that. 

If there's some feedback from the client but you're not sure what to do about it, because there are multiple options, comment on the JIRA issue presenting what options there are, estimating how much time each of it would take and maybe advising towards one of it and ask the PM to take the decision.

If in doubt, ask for a video call to discuss things. However, try to write down the notes / conclusions of the meeting, so you have them in writing. This helps you not forget anything and it also helps to align everyone on the team to the same conclusion.

# Further reading

* [VIPER architecture](./ViperArchitecture.md)
* [Modular architecture](./ModularArchitecture.md)
* [Code Modes](https://github.com/nodes-projects/readme/blob/master/mobile/ios/code-modes.md) (private document)
* [Securing your app](https://github.com/nodes-projects/readme/tree/master/security) (private document)
* Consider joining one or more of our [squads](https://github.com/nodes-projects/squads) (private document)
