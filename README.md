This document is meant for developers. It shows how we work at Nodes. 

# Nodes iOS


We love what we do and care about the products we create. They are a team effort, together with our designers, backend developers, project managers, and all the other people at Nodes. 

We try to write clean code and separate the pieces of code that occur often in our apps into separate libraries that can be reused in other projects. Our open source activity can be found on [GitHub](https://github.com/nodes-ios).

We try to increase our contribution to the iOS developer community through:

- abstracting relevant parts of our code and turning them into open source libraries that other developers can use
- encouraging our team members to join iOS related meetups, groups and conferences
- encouraging our team members to speak at iOS events
- contributing back to some of the other open source libraries we use through issues and PRs
- encouraging our team members to write tech articles about any topic they desire on our [engineering blog](https://engineering.nodesagency.com/); if needed, we can also suggest topics for new articles

We create lots of apps for our clients. Most of those apps rely heavily on web APIs. We abstracted the common operations for working with web APIs, and that's how [Serpent](https://github.com/nodes-ios/Serpent) (formerly known as Serializable) and [Cashier](https://github.com/nodes-ios/Cashier) were born. Another issue that was common in all the apps we do was handling keyboard appearance events. This led to the appearance of [KeyboardHelper](https://github.com/nodes-ios/KeyboardHelper).


# Team meetings
Here are the recurring meetings the iOS team takes part in:

#### iOS Team Meeting
This is the main meeting in the iOS team, where we talk about the latest things happening in our team. General direction of the team, brief general team performance review, what people need help with, amount of workload, should we use or not _that_ framework, etc. This happens in the first Monday of each month. 

#### Friday Tech Talk
This is a monthly meeting, that occurs on the fourth Friday of every month. Anyone in the engineering team can talk about anything cool that they implemented recently. It could be using some new technology, some cool framework, a nice animation, a clever algorithm or anything similar to this. The meeting is held in the Copenhagen office, but if anyone from other offices wants to attend, we can enable a video call.

#### Monthly Briefing

This is a monthly meeting, where the management tells all the employees how the company did in the last month and what our targets and short, mid and long-term plans are. Topics covered are sales, projects, cases, tech, events, staff and others. The meeting is held in the Copenhagen office, but other offices can join in by video call.


# Your First Day

The IT department is responsible for setting up accounts and giving you access to the tools you need to do your job. The easiest way to contact the IT departmentis by using the `/halp` command on Slack.

- Meet with the Head of iOS, your Team Manager (Lead Developer) and your Nodes Buddy. They will be your first persons of reference in the company. Use them as much as you need to get settled in, but also be considerate of their own time.
- Join [our private git](https://github.com/nodes-projects). Ask IT if you don't have access.
- Get the cert sign request and private key from [this private repo here](https://github.com/nodes-projects/keyring-ios). Add the private key to your Keychain and from now on, always use this certificate signing request when creating new certificates on the developer portal. 
- Install the latest Xcode. Ideally, from the [Apple developer portal](https://developer.apple.com/download/more/) and not from the App Store. If you got it from the App Store, that's ok too.
- Get another iOS developer to invite you to our developer accounts.
- We want you to help us make great open source software. So get another iOS developer to invite you to  [our GitHub organisation](https://github.com/nodes-ios). Make sure you enable your 2FA on GitHub. Our client projects are on [our private git](https://github.com/nodes-projects) and our public ones are on [GitHub](https://github.com/nodes-ios).
- Set up your git keys properly, so you can pull and push from both git servers.
- You should have been invited to our Slack, JIRA, and Postman accounts. Ask IT if you don't have access.
- Make sure to read the [Nodes Handbook](https://docs.google.com/document/d/1E4ZyGqIKDttGlJ0c0rEkNy2lxP-n1PBwQzuaESbLnpw/edit) (private document). That is meant for all employees, and tells a bit of our history, how we got here, but also how we handle different tasks.
- We use [Happeo](https://app.happeo.com/home) for internal (semi)official announcements. Ask IT if you don't have access.

# Tools We Use

For employee management we use [BambooHR](https://nodesagency.bamboohr.com/home). Ask IT if ou don't have access and the Chief People Officer if anything in there is unclear. Use this to request time off, register sick day and manage your personal info and banking info for salary pay.

Our main communication tool is [**Slack**](https://nodes.slack.com). We use this for daily communication.

Our main project management tool is [**JIRA**](https://nodesagency.atlassian.net/jira/). Each project has its own JIRA board. Always keep your project's JIRA board up to date to reflect the current status of the project. We work in an agile manner and move fast, but the JIRA board must clearly reflect the project's status. Ask [Simon](https://nodes.slack.com/messages/@siej) or your project manager if you have questions.

With the same JIRA account you will also have access to Confluence, where you can find project-related documentation, and also internal docuements.

[**Harvest**](https://nodes.harvestapp.com/) is the time tracking tool that we use. It helps us see how much time one person has worked on a project. Make sure to always harvest on the appropriate project. Ask the PM on which Harvest project you should track the time. We expect you to harvest 7.5 hours per day. Lunch time is not harvested, and it doesn't count towards the 7.5 hours per day. And if you want more detailed instructions on how to harvest, ask [Simon](https://nodes.slack.com/messages/@siej). You can also set up auto-harvesting in you Ournodes acount and it will automatically harvest 7.5 hours per day on the project youre assigned to.

Harvest goes well hand in hand with [**Forecast**](https://forecastapp.com/). Use Forecast to see what project you're assigned to that day. Forecast is our planning tool, you can see what other people are assigned to, how long a project should take, when other people are on vacation, etc. On a higher level, Harvest and Forecast are very well integrated and Project Managers can see if a project goes over budget (more hours were harvested than allocated in Forecast). But that's not something you as a developer should care about.

[**Postman**](https://www.getpostman.com/) is a great tool which helps you see and test web APIs. Our backend team uses Postman to test and document their APIs, so all the web APIs for our apps can be found in Postman. You can use it to see the different endpoints available, read their documentation or make requests to those endpoints. Ask IT if you don't have access.

Our design team uses Sketch. But you, as a developer, don't need to have Sketch installed. To ease the collaboration between designers and developers, we use [**Zeplin**](https://zeplin.io/). In Zeplin, you can see each screen in the design, get info about the sizes, padding, fonts, colours and also export assets for the mobile devices. You can also add notes in Zeplin and communicate with your designer directly on the project.

[**Charles**](https://www.charlesproxy.com/) is an HTTP proxy. You can set your phone / simulator to proxy through Charles and you can see all the API calls it made, you can inspect its requests or responses. It comes in very handy especially if you work with an external, poorly documented API. Ask IT if you need a license.

For in-house distribution and crash reporting, we use [**Firebase**](firebase.google.com/). Depensing on the project, sometimes we only use TestFlight. Talk to your PM or with previous developers on that project.

We had been using [**Carthage**](https://github.com/Carthage/Carthage) for a long time to manage our dependencies on iOS. We chose Carthage over CocoaPods because for us, this is the one that brought the most advantages. But since we started using Firebase more and more and Google pushes strongly for CocoaPods, we sometimes use both in the same project. We appreciate all the effort put into Carthage, as well as into CocoaPods, and we're looking for the right time to switch to Swift Package Manager as our default dependency manager for iOS projects.

The way we do localisation in Nodes is a bit different than in other places. We use [**NStack**](https://nstack.io/), a service we built, which together with the [**NStack SDK**](https://github.com/nstack-io/nstack-ios-sdk) offers dynamic localisation for our apps. Go to [nstack.io](https://nstack.io/), log in with your Nodes account, select the app you need (or create a new one), go to "Translate" and add new translations or edit the current ones. A translation consists of a key (by which the string is recognised through the SDK) and one or more values (depending on the number of languages your app is translated to). The translations can be changed in NStack and the changes will reflect in the app without the need of an app update.


# Coding Guidelines
Make sure to read our [**Swift Style Guide**](styleguide.md).  


# Continuous Integration (CI)

As a digital agency we build hundreds of apps during the day and to manage all these builds we are using Bitrise as a CI tool to speed up our deployment process and [Match](https://docs.fastlane.tools/actions/match/) + Github to manage our client's certificates.

Please find below the steps to configure your project.

***1) Creating a new project on Bitrise***

Once you get access to Bitrise the creation process is straightforward and most of it is automatic if you have attached your github account to your Bitrise account. 

[Here](./ci/bitrise-setup-readme.md) you will find a configuration guide to help you setting up your project on Bitrise.

***2) Integrating into your Xcode project***

If you already have a project created an you just need to deploy it to Bitrise you'll need to add the configuration file `project.yml` to the root of your project. In case you need to add or change any configuration but are unsure how to do that please refer to this [document](./ci/bitrise-config-readme.md).

***3) Troubleshooting***

We also listed the most common issues when Bitrise is trying to make the builds. Please check the [common issues document](./ci/bitrise-issues-readme.md) if you are having some problems.


# Working with Remote Colleagues

Having offices in 7 locations in Europe and Middle East means you get to work with colleagues who are not in the same office as you are. If that is the case, make sure to rely as much as possible on JIRA. 

Our main means of communication inside the company is Slack. Use it wisely.

It helps a lot to try and change your mindset from synchronous communication to asynchronous communication. This means that you try to foresee any problems you might run into and ask about info for them before you actually run into them. Try not to get into a situation where you need an answer from someone in order to be able to continue.

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
