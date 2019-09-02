# Nodes iOS Bitrise - Setup Guide 🛠

Setting up Bitrise is simple and we described in 3 steps:

- [Xcode setup](#Xcode-setup)
- [App setup on Bitrise](#App-setup-on-Bitrise)
- [Bitrise workflow integration](#Bitrise-workflow-integration)

## Xcode setup

Make sure your project's schemes are ***shared (including app extensions)*** , otherwise you will run into a lot of warnings and it might not build all of your targets.


## App setup on Bitrise

1) Create a *New App* from the Bitrise dashboard
- Make sure you choose **Nodes** account when creating the *New App* and make it **Private**

<p align="center">
  <img src="../images/ci/01-new-app-bitrise.jpg?raw=true" alt="New App"/>
</p> 

2) Connect the repository to Bitrise

<p align="center">
  <img src="../images/ci/02-new-app-bitrise.jpg?raw=true" alt="New App"/>
</p> 

3) When setting up the access make sure to add our SSH key using the private key found in the [ci-resources-ios](https://github.com/nodes-projects/ci-resources-ios/blob/master/privatekey) repository.

<p align="center">
  <img src="../images/ci/03-new-app-bitrise.jpg?raw=true" alt="New App"/>
</p> 

4) Indicate which branch Bitrise should use to make the builds

<p align="center">
  <img src="../images/ci/04-new-app-bitrise.jpg?raw=true" alt="New App"/>
</p> 

5) After choosing the branch, Bitrise will validate the source code and then you can select the *export method* you want to use. Usually is **app-store**

<p align="center">
  <img src="../images/ci/05-new-app-bitrise.jpg?raw=true" alt="New App"/>
</p> 

6) The last step is the Webhook setup. It will create a link from the github repository to Bitrise.

<p align="center">
  <img src="../images/ci/06-new-app-bitrise.jpg?raw=true" alt="New App"/>
</p> 


## Bitrise workflow integration

In order to make everything work on Bitrise you'll need to copy the template content from [bitrise.yml](https://github.com/nodes-projects/ci-resources-ios/blob/master/bitrise.yml) into the Bitrise workflow script.

You can find the detailed workflow description [here](https://github.com/nodes-ios/bitrise-step-nodes-custom-script)

<p align="center">
  <img src="../images/ci/07-new-app-bitrise.jpg?raw=true" alt="New App"/>
</p> 
