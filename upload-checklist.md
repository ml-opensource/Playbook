# Upload Checklist

These are the requirements for an app to be submitted to the store. Unless you get an explicit exception from QA and the PM, these requirements must be fulfilled. If some are missing tickets, add them yourself and notify the PM so everyone is aware of the extra time needed before submitting. 

## Tools/Frameworks 
* Hockey crash reporting.
* Google Analytics
	* [More info here](https://github.com/nodes-projects/readme/blob/master/mobile/analytics.md)
	* If there is no ticket for analytics and/or the client "doesn't care," we will still complete the **Default tracking** listed in the link above.
* NStack
	* The App open `NStack.start()` call is required, even if we are not using NStack translations or other features.
	* Version control should be tested and working.
	* N-meta header must be included in API calls (See the [Nodes framework](https://github.com/nodes-ios/Nodes) for info).
*  New relic, if the app communicates with an API that Nodes did not develop.


## UI
* Version number info somewhere in the settings.
* No hardcoded text.
* App functions offline with cached data.
* Similarly, if there is no data, there must be UI for an empty view
	* The design team does not always create these views. At a minimum, there should be a label saying there is no data to display. 
*  Keyboards should not block content. Views with keyboards must either fit the entire UI above the keyboard area, or become scrollable while the keyboard is visible. 
*  For updates to existing apps: cached data should persist across versions. Users should not need to log in again when they update the app. 


## Project
* README.md on github.
* Build runs on the CI.
* Staging and Production environments are separated and handled appropriately (not just by commenting out lines of code).

___
# Extra features

At Nodes, we pride ourselves on creating awesome app experiences. The following checklist items are not *required* for an app upload, but are a reflection of the quality we expect to deliver. QA *will* make tickets for these and flag them as issues, and developers at Nodes are expected to complete these tasks even if there isn't a ticket. 

* Pull to refresh on lists, and pagination where appropriate. 
* Native UI behavior works as expected:
	* Swipe to go back in a navigation stack
	* Buttons show a pressed state (even just the default)
	* Table view cells select/deselect
	* Form entry views should have keyboards with Next and Done/Continue buttons
* Views transition appropriately and do not immediately flash on screen in one frame. This includes switching from a login to main flow when replacing the window/root VC. 
* Loading indicators or skeleton views anytime UI is dependent on an API call. 
	* Do not block the entire UI with a spinner unless absolutely necessary. Users should still be able to cancel or go back, and the UI should display what it can with the data it has (this is why skeleton views are preferred). 
* When uploading data, the app should display the local version of the new data while waiting for the API to return, and not show blank data. 