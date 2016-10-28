# Swift Style Guide

We don't enforce a strict style guide. The rule of thumb for the style of our Swift code is common sense. 

This document is a continous work in progress. When we discover a better way to do thigs, we update our coding style guide.

We suggest those guidelines because, if everyone in the team uses the same guidelines, it's much easier for one to work on another's project. 

## Structure

### Project

* We usually name the class that takes care of the networking layer `ConnectionManager`. 
* The models will have descriptive, simple names: `User`, `Post`, `NewsItem`, `Bird`, etc. 
* Usually, anything that is not a model should have some suffix indicating what it is: `RoundedButton`, `CacheManager`, `DeepLinkManager`. There are a few exceptions. Some of our projects use a `Router` which takes care of the screen flow in the app, for example.
* All the custom views should end in `View`: `NewsItemView`, `PensionItemView`, etc. This clearly separates them from the model, but also indicates what that view does.
* Similarly, all custom buttons end in `Button`, all custom cells end in `Cell`, all custom labels end in `Label`, all custom something ends in that something. 
* All view controllers end in `VC`. `LoginVC`, `TermsVC`, `HelpVC`, etc. We prefer `VC` over `ViewController` because it's shorter

### File

Use `//MARK: - ` comments to separate the different parts of your code. 

```swift
class MainVC : UIViewController {
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
Of course, you can use other `//MARK: -` comments too, as long as they are easy to understand and improve the readability of the code.

## Extensions
When adding a protocol implementation to a class or struct, add a separate extension for the protocol methods and use the `//MARK: - ` comment. This increases the readability of the code. 

```swift
class MainVC : UIViewController {
    // ...
}

// MARK: - UITableViewDataSource
extension MainVC : UITableViewDataSource {
    // table view data source methods
}
```

## Naming
The classes, structs, protocols, methods, variables, etc. must have descriptive names. Method names and variables must start with a lower case letter. Classes, structs, type names, enums should be capitalized. 
The name of a variable should be enough to tell another programmer what that variable does. Don't use variable names such as `number`, `a`, `b`, `x`, `button`, `label`, etc. To adhere to the Swift 3 syntax, all enum cases will be lowerCamelCase and not UpperCamelCase as before. 

## Classes and Structs
Use structs over classes, whenever it is possible. Unless you really need inheritance, or Objective-C compatibility, use a struct and not a class.

## Access control
Specify access control to each top-level variable and functions. 

## Storyboards and nibs
We encourage usage of Storyboards and Nibs. They help a new developer on the project understand the codebase and see the bigger picture faster than just code. 

However, please don't set the fonts and colors in the storyboard.

## Colors and fonts
Create categories for UIFont and UIColor with the app's fonts and colors. Zeplin helps with that, and you can export the categories directly from there. 

Always set the fonts and colors in code, using the ones from the categories. A good place to do that is in the `didSet` of the `IBOutlet`s or variables.

Setting them in code allows you to change them really quickly and easily, in all the appropriate places, if it's decided for example to change a color with a darker one. 

## Other guidelines
* Use `let` and not `var` wherever possible
* Use `guard let` wherever appropriate
* Avoid pyramids of doom. Unwrap multiple optionals on the same line and mix it with logical conditions as needed.

 ```swift
 if let age = age, let name = name where name.characters.count > 0 && age.characters.count > 0 {
     //...
 }
```
Remember you can also do things like

 ```swift
 if !myAutoFailCondition, let foo = expensiveCall() {
     //...
 }
```
* Try to have as few warnings as possible. Ideally, there would be no warnings. But we all know it's hard to have that. It's not a big deal if there are some warnings in the code, but fix right away warnings referring to usage of `var` for a variable that could've been a `let`, unused variables that can be replaced with `_`, unreachable code, or old syntax fo selectors.
* Don't leave out commented code. Or if you feel you really need to, also leave a comment saying why that code is there and why it might be needed again. But in general, delete commented out code. We use git, so you can always get old code from there.