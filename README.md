This document is meant for developers. It shows how we work at Nodes. 

# Nodes iOS


We love what we do and care about the products we create. They are a team effort, together with our designers, backend developers, project managers, and all the other people at Nodes. 

We try to write clean code and separate the pieces of code that occur often in our apps into separate libraries that can be reused in other projects. Our open source activity can be found on [GitHub](https://github.com/nodes-ios).

We try to increase our contribution to the iOS developer community through:

- abstracting relevant parts of our code and turning them into open source libraries that other developers can use
- encouraging our team members to join iOS related meetups, groups and conferences
- encouraging our team members to speak at iOS events
- contributing back to some of the other open source libraries we use through issues and PRs
- encouraging our team members to write tech articles about any topic they desire on our [engineering blog](https://engineering.nodesagency.com/)

We create lots of apps for our clients. Most of those apps rely heavily on web APIs. We abstracted the common operations for working with web APIs, and that's how [Serpent](https://github.com/nodes-ios/Serpent) (formerly known as Serializable) and [Cashier](https://github.com/nodes-ios/Cashier) were born. Another issue that was common in all the apps we do was handling keyboard appearance events. This led to the appearance of [KeyboardHelper](https://github.com/nodes-ios/KeyboardHelper).

We are currently in the process of abstracting parts of our codebase into open source libraries that can be reused in other projects. As well as this, we are trying to change our way of thinking for current and future projects and when we encounter a feature whose implementation can be reused in other projects we try to implement it as a separate component which we open source. We are just beginning, and it is a big change, but this is what we aim for in the long run.


# Team meetings
Here are the recurring meetings the iOS team takes part in:

#### iOS Team Meeting
This is the main meeting in the iOS team, where we talk about the latest things happening in our team. General direction of the team, brief general team performance review, what people need help with, amount of workload, should we use or not _that_ framework, etc. This happens in the first Monday of each month. 

#### Mobile Show and Tell Meeting
This is a monthly meeting, that occurs on the third Friday of every month. Members of the iOS and Android team talk about anything cool that they implemented recently. It could be using some new technology, some cool framework, a nice animation, a clever algorithm or anything similar to this. Traditionally, there's beer for presenters and attendees. 

Besides the team meetings, we also have two more larger meetings we take part in.

#### Monthly Tech Talks

Thr Tech Talks is a monthly meeting where all our develoeprs and QA take part. Each month, another team has the agenda, and they talk about something relevant to their domain, but which can affect all of us. We try to maximize the knowledge sharing so we can all become better together. 

#### Quarterly Company Catch-up

This is a quarterly meeting, where the board tells all the employees how the company did in the last quarter and what our targets and short, mid and long-term plans are. You'll find out if the sales and production are on track, below or ahead of target, and anything else relevant to the company. It's not only a presentation, feel free to ask questions. 




# Your First Day
- Join [our private git](https://git.nodescloud.com) and ask [Dominik](https://nodes.slack.com/messages/@doha) to add you to the correct groups.
- Get the cert sign request and private key from [this private repo here](https://git.nodescloud.com/ios/Keyring). Add the private key to your Keychain and from now on, always use this certificate signing request when creating new certificates on the developer portal. 
- Install the latest Xcode. Ideally, from the [Apple developer portal](https://developer.apple.com/download/more/) and not from the App Store. If you got it from the App Store, that's ok too.
- Get another iOS developer to invite you to our developer account.
- We want you to help us make great open source software. So get another iOS developer to invite you to  [our GitHub organisation](https://github.com/nodes-ios). Make sure you enable your 2FA on GitHub. Our client projects are on [our private git](https://git.nodescloud.com) and our public ones are on [GitHub](https://github.com/nodes-ios).
- Set up your git keys properly, so you can pull and push from both git servers.
- Ask an iOS colleague to invite you to Hockey
- Ask [Casper](https://nodes.slack.com/messages/@cr) for access to Postman
- Have a project manager add you to our Trello organisation
- Ask [Jonas](https://nodes.slack.com/messages/@josc) to add you to Slack. Make sure to join the following channels: [#ios](https://nodes.slack.com/messages/ios), [#ios-core](https://nodes.slack.com/messages/ios-core), [#mobile](https://nodes.slack.com/messages/mobile), [#nodes-cph](https://nodes.slack.com/messages/nodes-cph) (if you're in Copenhagen), [#team-nodes-uk](https://nodes.slack.com/messages/team-nodes-uk) (if you're in London). Also join any project channel that you're working on.
- Make sure to read the description of our [iOS stack on our engineering blog](https://engineering.nodesagency.com/our-stacks/ios/). That article goes hand in hand with this playbook here.
- Make sure to read the [Nodes Handbook](https://docs.google.com/document/d/1E4ZyGqIKDttGlJ0c0rEkNy2lxP-n1PBwQzuaESbLnpw/edit) (private document). That is meant for all employees, and tells a bit of our history, how we got here, but also how we handle different tasks.
- We love eating cake, and we hope you do too. We'll use any excuse to do it. So we'll ask you to have [Simon](https://nodes.slack.com/messages/@siej) add your birthday to the calendar, so we can get you a big birthday cake and celebrate.
- We have Facebook groups for internal semi-official announcements. Ask a colleague to add you to the groups. 

# Tools We Use
Our main communication tool is [**Slack**](https://nodes.slack.com). We use this for daily communication.

Our main project management tool is [**Trello**](https://trello.com). Each project has its own Trello board. Always keep your project's Trello board up to date to reflect the current status of the project. We work in an agile manner and move fast, but the Trello board must clearly reflect the project's status. Ask [Simon](https://nodes.slack.com/messages/@siej) or your project manager if you have questions.

[**Basecamp**](https://basecamp.com) is the main tool through which we interact with the clients. As a developer, normally you shouldn't have to deal that much with the clients directly or through Basecamp, but each project is unique and in some cases, developers are also added to Basecamp.

[**Harvest**](https://nodes.harvestapp.com/) is the time tracking tool that we use. It helps us see how much time one person has worked on a project. Make sure to always harvest on the appropriate project. Ask the PM on which Harvest project you should track the time. We expect you to harvest 7.5 hours per day (it's ok to do more, if you want). Lunch time is not harvested, and it doesn't count towards the 7.5 hours per day. And if you want more detailed instructions on how to harvest, ask [Simon](https://nodes.slack.com/messages/@siej).

Harvest goes well hand in hand with [**Forecast**](https://forecastapp.com/). Use Forecast to see what project you're assigned to that day. Forecast is our planning tool, you can see what other people are assigned to, how long a project should take, when other people are on vacation, etc. On a higher level, Harvest and Forecast are very well integrated and Project Managers can see when a project goes over budget (more hours were harvested than allocated in Forecast). But that's not something you as a developer should care about.

[**Postman**](https://www.getpostman.com/) is a great tool which helps you see and test web APIs. Our backend team uses Postman to test and document their APIs, so all the web APIs for our apps can be found in Postman. You can use it to see the different endpoints available, read their documentation or make requests to those endpoints. If you don't already have access, ask Casper or Jonas for an invite to Postman.

Our design team uses Sketch. But you, as a developer, don't need to have Sketch installed. To ease the collaboration between designers and developers, we use [**Zeplin**](https://zeplin.io/). In Zeplin, you can see each screen in the design, get info about the sizes, padding, fonts, colours and also export assets for the mobile devices. You can also add notes in Zeplin and communicate with your designer directly on the project.

[**Charles**](https://www.charlesproxy.com/) is an HTTP proxy. You can set your phone / simulator to proxy through Charles and you can see all the API calls it made, you can inspect its requests or responses. It comes in very handy especially if you work with an external, poorly documented API. 

For in-house distribution and crash reporting, we use [**Hockey**](https://www.hockeyapp.net/). You need to be invited to our company's account. Ask any other iOS developer for an invite. We're currently considering replacing Hockey with another similar service; we will update this document when/if we do it.

We use [**Carthage**](https://github.com/Carthage/Carthage) to manage our dependencies on iOS. We chose Carthage over CocoaPods because for us, this is the one that brought the most advantages. We appreciate all the effort put into Carthage, as well as into CocoaPods, and we're looking forward to Swift Package Manager becoming the default dependency manager for iOS projects.

The way we do localisation in Nodes is a bit different than in other places. We use [**NStack**](https://nstack.io/), a service we built, which together with the [**NStack SDK**](https://github.com/nodes-ios/NStack) offers dynamic localisation for our apps. Go to [nstack.io](https://nstack.io/), log in with your Nodes account, select the app you need (or create a new one), go to "Translate" and add new translations or edit the current ones. A translation consists of a key (by which the string is recognised through the SDK) and one or more values (depending on the number of languages your app is translated to). The translations can be changed in NStack and the changes will reflect in the app without the need of an app update.



# Coding Guidelines
Make sure to read our [**Swift Style Guide**](styleguide.md).  


# Nodes CI
The Nodes CI is our new continuous integration tool. This was built mostly by Dominik, with help from Kasper. Since it's still new, we don't really use it in many of our projects. However, all the new projects should have CI set up. [Here](https://engineering.nodesagency.com/articles/iOS/Continuous-Integration-on-iOS-with-HockeyApp-and-Testflight-Deployment/) you can find an article about how we got to build our own CI system. [Here](https://git.nodescloud.com/ios/ci-template) you can find a template for implementing our CI in your project.

# Swift Migration Guide

A guide that shows how to migrate between different versions of Swift in our projects can be [found here](#migration-guide.md).

# Working with Remote Colleagues
Having one office in London, one in Copenhagen and one in Aarhus means you get to work with colleagues who are not in the same office as you are. If that is the case, make sure to rely as much as possible on Trello. 

Our main means of communication inside the company is Slack. Use it wisely.

It helps a lot to try and change your mindset from synchronous communication to asynchronous communication. This means that you try to foresee any problems you might run into and ask about info for them before you actually run into them. Try not to get into a situation where you need an answer from someone in order to be able to continue.

Always have a good overview of what's left to be done and what you need in order to get it done. 

If you need something (an image asset, some input from the PM, etc), make a Trello card asking for that. 

If there's some feedback from the client but you're not sure what to do about it, because there are multiple options, comment on the Trello card presenting what options there are, estimating how much time each of it would take and maybe advising towards one of it and ask the PM to take the decision.

If in doubt, ask for a video call to discuss things. However, try to write down the notes / conclusions of the meeting, so you have them in writing. This helps you not forget anything and it also helps to align everyone on the team to the same conclusion.
