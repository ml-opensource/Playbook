
## 📖 Modular Project architecture

With the addition of SPM, we now aim to modularise our projects as much as possible. The [iOS project template](https://github.com/nodes-ios/ios-template) gives a great starting point on how to do this. Our aim is to modularise all code, meaning all code can be set in standalone features and modules that can be run and tested independetly in isolation from the rest of the code base. This approach forces us to build simpler code that is less likely to have hidden implicit dependencies that may complicate features unnecessarily.

Before developing with this modularised approach, you should watch both part 1 & 2 of the [point free episodes](https://www.pointfree.co/episodes/ep171-modularization-part-1), which explain more on the advantages of this approach and how to do it.

--

### Project structure

The template project consists of several base modules

- APIClient Module
	- In charge of handling any communication to backend APIs for any required configurations
    - Ability to provide mock & preview responses

- APIClientLive Module
	- Holds all the DTO models
	- Handles building required URLRequests with authentication
    - Handles the decoding of request responses    

- AppFeature Module
	- The main entry point module for the application
 
- Localizations Module
    - Handles localizations across the app, in most cases using NStack
    - Provides ObservableLocalizations class allowing for SwiftUI to use Localizations confirming to the `ObservableObject` protocol 
    
- Model Module
    - Contains all models used for managing data
    
- NetworkClient Module
    - A helper class to observe network changes
    
- PersistenceClient Module
    - For persisting/caching data throughout the application
    
- Style Module
    - For managing and accessing Fonts, Colors, Assets
    - For core standard common UI such as Alert & ButtonStyles

The template has example modules of features your app may require;
- LoginFeature Module
- MainFeature Module
 
Other more straightforward modules include;
- AppVersion Module
- Helpers Module

--

<b>Summary</b>:

- Separation of concerns and decoupling
- Improved reusability
- Improved testability

## Testing

Using a modular architecture, everything is easy to test since it is based on SRP (Single Responsibility Principle). The template contains great examples on how to add test targets to the package.swift file. 

```swift
        .testTarget(
            name: "LoginFeatureTests",
            dependencies: [
                "LoginFeature", .product(name: "CombineSchedulers", package: "combine-schedulers"),
            ]),
```
