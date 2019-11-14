# Swift Style Guide

We don't enforce a strict style guide. The rule of thumb for the style of our Swift code is common sense. 

This document is a continuous work in progress. When we discover a better way to do thigs, we update our coding style guide.

We suggest those guidelines because if everyone in the team does things in a similar way, it's much easier for one to work on someone else's project. 

These guidelines will, of course, not cover every aspect of writing Swift code. If you're unsure about something, either refer to the [Ray Wenderlich Swift style guide](https://github.com/raywenderlich/swift-style-guide) or ask in the Slack channel.

Always adhere to the Swift official [API design guidelines](https://swift.org/documentation/api-design-guidelines/).

Check out [this readme](https://github.com/nodes-ios/VIPERCoordinatorsXcodeFileTemplate/blob/master/README.md) and [this talk by @doha](https://slideslive.com/38908270/architecting-your-app-with-viper-effectively) for an explanation of how we use VIPER architecture at Nodes.

The template should provide most of the style reference you should follow when adopting this architecture. 


## Structure

### Project

The following guidelines (most of which will be repeated further down in this document) should give you some tips that will make it easier for you to navigate through the project.


* The models will have descriptive, simple names: `User`, `Post`, `NewsItem`, `Bird`, etc. When working with a Nodes backend made in Vapor, it's helpful to ask them for their model, as it will closely resemble ours. 
* Usually, anything that is not a model should have some suffix indicating what it is: `RoundedButton`, `CacheManager`, `DeepLinkManager`. There are a few exceptions. Follow the Swift API design guidelines with regards to this rule. 
* All the custom views should end in `View`: `NewsItemView`, `PensionItemView`, etc. This clearly separates them from the model but also indicates what that view does.
* Similarly, all custom buttons end in `Button`, all custom cells end in `Table/CollectionViewCell`, all custom labels end in `Label`, all custom something ends in that something. 
* All view controllers end in `ViewController`. These should be created for you automatically by our template. 

### File

Use `// MARK: - ` comments to separate the different parts of your code. Some of these are provided automatically by the template. 


### Line length

Some languages use 80 characters as the line length, but we feel that is too short for a verbose framework like UIKit. Our swiftlint.yml file sets the limit at 120 lines. If you set your page guide in Xcode preferences to 100, it will give you a bit of a buffer. 

There are two common ways to add line breaks to long lines. We haven't decided on a final solution, so just be consistent. 


Examples:

Xcode default:

```swift
tableView.tableHeaderView = UIView(frame: CGRect(x: 0,
                                                 y: 0,
                                                 width: 0,
                                                 height: 0))

func tableView(_ tableView: UITableView,
               cellForRowAt indexPath: IndexPath) -> UITableViewCell {
   // ...
}

```

Vapor's line break strategy: 

```swift 
tableView.tableHeaderView = UIView(
	frame: CGRect(
		x: 0, 
		y: 0, 
		width: 0, 
		height: 0
	)
)

func tableView(
	_ tableView: UITableView, 
	cellForRowAt indexPath: IndexPath
) -> UITableViewCell { 
	...
}



```

## Extensions
When adding a protocol implementation to a class or struct, add a separate extension for the protocol methods and use the `// MARK: - ` comment. This increases the readability of the code. Try not to conform to protocols in the initial class/struct declaration (`Codable` is an exception for example). 

```swift
class MainViewController: UIViewController {
    // ...
}

// MARK: - UITableViewDataSource
extension MainViewController: UITableViewDataSource {
    // table view data source methods
}
```

## Naming
* The classes, structs, protocols, methods, variables, etc. must have descriptive names. 
* Method names and variables must start with a lower case letter. 
* Classes, structs, type names, enums should be capitalized. 
* The name of a variable should be enough to tell another programmer what that variable does. Don't use variable names such as `number`, `a`, `b`, `x`, `button`, `label`, etc. 
* To adhere to modern Swift syntax, all enum cases should be lowerCamelCase and not UpperCamelCase as before. 
* Don't use snake_case.
* Don't prefix your classes or structs. Swift types are automatically namespaced by the module they're contained in, so there should be no collisions. 

## Classes and Structs
Where it makes sense, use structs over classes. Unless you really need inheritance or Objective-C compatibility, it's probably advisable to use a struct and not a class. And if you use classes but you don't need inheritance, consider making them `final`.

## Access control
Specify `private` functions and variables when applicable. Variables can almost always be `private` and injected via the initializer if needed. Computed properties are potentially an exception. Helper functions should be `private` if they are not called from outside the class.

The distinction between `open` `public` and `internal` is not as important for our development style at the moment so specifying `internal` is not necessary.

As of Swift 4, `fileprivate` is rarely required. 

## Storyboards and nibs
This is a conflicting topic in the iOS community. We encourage usage of Storyboards and Nibs. They help a new developer on the project understand the screen flow and the codebase and see the bigger picture faster than if they just read the code. The template will automatically create them for you for your viewcontrollers.

However, please don't set the fonts and colors in the storyboard. It's ok to do that to make the view more recognisable in the IB file, but always set the appearance in code too. 

## Colors and fonts
Create categories for UIFont and UIColor with the app's fonts and colors. Zeplin helps with that, and you can export the categories directly from there. 

Always set the fonts and colors in code, using the ones from the categories. A good place to do that is in the `didSet` of the `IBOutlet`s or variables. Another option is to have a `style()` method in your viewcontroller where you set all colors. We are still deciding which approach is better.

Setting them in code allows you to change them really quickly and easily, in all the appropriate places, if it's decided for example to change a color with a darker one. 

## Other guidelines
* Use `let` and not `var` wherever possible
* Use `guard let` wherever appropriate
* For pure constants, use enums without cases to namespace them. For example

```swift
enum Constants {
    enum Math {
        static let e = 2.71
        static let pi = 3.14
    }
    
    enum CacheKeys {
        static let feed = "feed"
        static let notifications = "notifications"
    }
}

print(Constants.Math.pi)
    
```
* Don't write unnecessary code. That includes declaring types that can be inferred or using shortcut versions of type declarations (`[String]` instead of `Array<String>`).
* Avoid using `self` where it doesn't need to be used.
* Use computed properties over functions if the operation can be done in O(1). For example

```swift
var diameter: Float {
    return radius * 2
}
```
Instead of 

```swift
func diameter() -> Float {
    return radius * 2
}
```

* Avoid pyramids of doom. Unwrap multiple optionals on the same line and mix it with logical conditions as needed. Prefer `guard` to `if` when possible. Examples with line breaks: 

    
    
```swift
// Default
guard let age = age,
    let name = name,
    !name.isEmpty,
    !age.isEmpty else {
    //...
}    
	
guard
    let age = age,
    let name = name,
    !name.isEmpty,
    !age.isEmpty
else {
    //...
}
	
```
Remember you can also do things like

```swift
 if !myAutoFailCondition, let foo = expensiveCall() {
     //...
 }
 
```

* Comments are for "why" and not just "what". It is often more helpful to explain why you made a complicated decision than to describe step-by-step what is going on. 
* Don't introduce new warnings. Sometimes warnings are understandable, if they come from a framework, shown as a //TODO, or were already in the project when you took over. But your code should always have the warnings resolved. A project *can* have 0 warnings.
* Don't leave commented code in. Or if you feel you really need to, also leave a comment saying why that code is there and why it might be needed again. But in general, delete commented out code. We use git, so you can always get the old code from there.
* If you need to check an enum case but you wouldn't want to do a switch for only one item, consider using something like `if case let .button = object.type { }`. It also works with associated values `if case let .button(value) = object.type { }`, and you can use `value` inside the `if`



## References
* [Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)
* [Ray Wenderlich Swift style guide](https://github.com/raywenderlich/swift-style-guide)
