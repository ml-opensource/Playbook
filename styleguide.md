# Swift Style Guide

We don't enforce a strict style guide. The rule of thumb for the style of our Swift code is common sense. 

This document is a continuous work in progress. When we discover a better way to do thigs, we update our coding style guide.

We suggest those guidelines because if everyone in the team does things in a similar way, it's much easier for one to work on someone else's project. 

These guidelines will, of course, not cover every aspect of writing Swift code. If you're unsure about something, either refer to the [Ray Wenderlich Swift style guide](https://github.com/raywenderlich/swift-style-guide) or ask in the Slack channel.

Always adhere to the Swift official [API design guidelines](https://swift.org/documentation/api-design-guidelines/).

**[UPDATE]**We are in the process of adopting a standard Clean Architecture pattern for all the new projects we do. It is possible that some of the existing guidelines here will conflict with the new approach we are trying. It is too early now to write guidelines for that, but as soon as we have a clear agreement on some standards for the new Clean Architecture approach, we will write them down.

TODO: 	Models layout, Actions enums vs protocol methods, Display data, ? 


## Structure

### Project

The following guidelines (most of which will be repeated further down in this document) should give you some tips that will make it easier for you to navigate through the project.

* **[UPDATE]**We usually name the class that takes care of the networking layer `ConnectionManager`. 
* The models will have descriptive, simple names: `User`, `Post`, `NewsItem`, `Bird`, etc. 
* Usually, anything that is not a model should have some suffix indicating what it is: `RoundedButton`, `CacheManager`, `DeepLinkManager`. There are a few exceptions. **[UPDATE]**Some of our projects use a `Router` which takes care of the screen flow in the app, for example.
* All the custom views should end in `View`: `NewsItemView`, `PensionItemView`, etc. This clearly separates them from the model but also indicates what that view does.
* **[UPDATE]**Similarly, all custom buttons end in `Button`, all custom cells end in `Cell`, all custom labels end in `Label`, all custom something ends in that something. 
* **[UPDATE]**All view controllers end in `VC`. `LoginVC`, `TermsVC`, `HelpVC`, etc. We prefer `VC` over `ViewController` because it's shorter

### File

Use `// MARK: - ` comments to separate the different parts of your code. 

**[UPDATE]**

```swift
class MainViewController: UIViewController {
    // MARK: - Outlets
    @IBOutlet weak var scrollView: UIScrollView!
    //...
    
    // MARK: - Properties
    private var shouldRefresh = false
    //...
    
    // MARK: - View
    override func viewDidLoad() {
        super.viewDidLoad()
        //...
    }
    
    override func viewWillAppear(animated: Bool) {
        super.viewWillAppear(animated)
        //...
    }
    //...
    
    // MARK: - Actions
    @IBAction func logonPressed(sender: AnyObject) {
        //...
    }
    
    // MARK: - Misc
    //...
    
}
```
Of course, you can use other `// MARK: -` comments too, as long as they are easy to understand and improve the readability of the code.


### Line length

Page guide at column: 100 (testing)

**[UPDATE]**
Examples:

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
When adding a protocol implementation to a class or struct, add a separate extension for the protocol methods and use the `// MARK: - ` comment. This increases the readability of the code. 

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
* **[UPDATE]**To adhere to the Swift 3 syntax, all enum cases will be lowerCamelCase and not UpperCamelCase as before. 
* Don't use snake_case.
* Don't prefix your classes or structs. Swift types are automatically namespaced by the module they're contained in, so there should be no collisions. 

## Classes and Structs
Where it makes sense, use structs over classes. Unless you really need inheritance or Objective-C compatibility, it's probably advisable to use a struct and not a class. And if you use classes but you don't need inheritance, consider making them `final`.

## Access control
Specify access control to each top-level variable and functions. Don't expose methods and variables that don't need to be public. 

## Storyboards and nibs
This is a conflicting topic in the iOS community. We encourage usage of Storyboards and Nibs. They help a new developer on the project understand the screen flow and the codebase and see the bigger picture faster than if they just read the code. 

However, please don't set the fonts and colors in the storyboard. It's ok to do that to make the view more recognisable in the IB file, but always set the appearance in code too. 

## Colors and fonts
Create categories for UIFont and UIColor with the app's fonts and colors. Zeplin helps with that, and you can export the categories directly from there. 

**[UPDATE]**Always set the fonts and colors in code, using the ones from the categories. A good place to do that is in the `didSet` of the `IBOutlet`s or variables.

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
* **[UPDATE]**Use computed properties over functions if the operation can be done in O(1). For example

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

* **[UPDATE]**Avoid pyramids of doom. Unwrap multiple optionals on the same line and mix it with logical conditions as needed.

 ```swift
 if 
 	let age = age, 
 	let name = name, 
 	name.characters.count > 0, 
 	age.characters.count > 0
 {
     //...
 }
 
 guard 
 	let age = age, 
 	let name = name, 
 	!name.isEmpty, 
 	!age.name.isEmpty
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
* **[UPDATE]**Try to have as few warnings as possible. Ideally, there would be no warnings. But we all know it's hard to have that. It's not a big deal if there are some warnings in the code, but fix right away warnings referring to usage of `var` for a variable that could've been a `let`, unused variables that can be replaced with `_`, unreachable code, or old syntax fo selectors.
* Don't leave commented code in. Or if you feel you really need to, also leave a comment saying why that code is there and why it might be needed again. But in general, delete commented out code. We use git, so you can always get the old code from there.
* If you need to check an enum case but you wouldn't want to do a switch for only one item, consider using something like `if case let .button = object.type { }`. It also works with associated values `if case let .button(value) = object.type { }`, and you can use `value` inside the `if`


### Delegation

TODO: 

## References
* [Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)
* [Ray Wenderlich Swift style guide](https://github.com/raywenderlich/swift-style-guide)