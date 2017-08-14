# Apple Developer Accounts 
# 🌟


## Roles

### Admins: 
* AMT 
* iOS Platform Lead 
* Operations 

### Members:
* Developers actively working on the project

## Process:

### AMT
AMT will add developers as members to the project team when they join the project, and remove them when they are no longer allocated to the project. They will also be in charge of monitoring expiring certitficates and profiles, and maintaining the device list. 

### iOS Platform Lead
The lead is in charge of the activities that require admin rights. This includes generating production certificates and profiles, approving signing requests. When a project is started, the lead will create the distribution certificate and profile and commit them to the project git repository. 

### Operations
Operations is the fail-safe, in case the lead or AMT are unavailable

# iTunes Connect Accounts

## Roles

### Admins:
* AMT 

### Developers:
* CI

## Process:

### AMT
AMT will manage app information and releases on behalf of Nodes, including project descriptions, Test Flight builds, and app submission. Project managers will take a less techincal role and therefore not need access to iTunes Connect. 

### CI
The Continuous Integration system will handle all uploads to Test Flight. Individual developers will use the CI system to upload builds, and therefore will not need access to iTunes Connect. 
