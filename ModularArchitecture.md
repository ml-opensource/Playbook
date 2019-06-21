
## 📖 Modular Project architecture

Most of Nodes applications are architected using 🐍 Viper Architecture, but as Apple is moving towards a more modular architecture, we are starting to adapt it in combination with Viper.

--

### Project structure

The project consists of several base modules

- Application Module
	- In charge of preseting the UI and navigation
	- Normally consisting of AppDelegate, UIViewControllers, Presenters, Coordinators
	- Initialises and handles dependencies in the application

- Data Module
	- Holds all the data models (fx. UserModel)
	- Takes care of API communications via an API layer (fx. ServerRepository)
	- Handles all data related operations via Interactors

- Core-UI Module
	- UI extensions
	- UIColor, UIFonts and custom styles declarations

- Core Module
	- Buissiness logic related extensions (fx. an extension on DateFormatter)
	- Core app functionality (fx. implementing Observable Pattern)

Based on the project needs and requirements you can create your own modules. One example could be having an app security module.


<b>In Detail</b>:

<b>The Application Module</b> is responsible of initialising the application and its dependencies and of handling view presentation and routing. The Dependencies, which are coming from the other modules, are interfaced in the application with the help of protocols.

--

<b>The Data Module</b> is resposible for handling the application data. Here we will create our data models (fx. UserModel, APIResponseModel etc.), Interactors, send requests to our API via our ServerRepository, perform caching operations, format application data with the help of designated structs (fx. a PriceFomatter to format all the prices in a Store like application).

This module will expose all its public functionality to the Application Module via protocols. For example, when communicating with the server we might require an UserServerRepository and an UserCacheRepository, which will be used in an UserInteractor in a VIPER like architecture, and which will handle all our user related API calls and cache calls.

An pottential UserServerRepository will expose the following protocol:

```swift
public protocol UserServerRepository {
    func getUser(with id: String) -> Promise<User>
    func updateUser(_ user: User)
}
```

--

<b>The Core-UI Module</b> is the place where we will declare our applications style, colors and fonts. As well here we can add extenstions on UIKit classes.

--

<b>The Core Module</b> is handling core functionality for our application. Here we can extend fx. Date and create convenience functions for working with Date in our application.

--

### Benefits of using modularity in code

By using a modular approach when developing our applications we are enforcing separation of concerns between features, because you will have to explicitly add modules as dependencies. As well having modules for an easier migration of the code accross different project. For example you might want to keep your Core and Core-UI module and reuse them in a new application. Modularity also allows us to focus on specific functionality when writing tests for our code, without having to create a lot of boilerplate to support testability.

<b>Summary</b>:

- Separation of concerns and decoupling
- Improved reusability
- Improved testability

## Testing

Using a modular architecture, everything is easy to test since it is based on SRP (Single Responsibility Principle).

For automated tests we suggest you to use Quick and Nimble framework.
