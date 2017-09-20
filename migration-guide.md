# Swift Migration Guide

This guide should help you with migrating projects on previous version of Swift to newer versions.

### Swift 2 → Swift 3

**IMPORTANT:** Make granular commits after each step and substep in this guide. Make sure the commit messages follow the proper rules.

1. Clone project and pull/checkout all branches ([script here](http://stackoverflow.com/a/21189710/1001803)).
    - Clean up all branches and keep only `master` and `develop`
    - Make sure `develop` is even or ahead of `master`
2. From `develop` branch run `git checkout -b feature/swift3-migration`.
3. *(optional)* Clean project, remove unused files, update file structure.
4. Update `Cartfile` to point to Swift 3 versions of dependencies. 📦 
    - Update framework names if used in project
        - `NStack` → `NStackSDK`
        - `Serializable` → `Serpent`
    - Remove existing Carthage folder and run `carthage update --platform ios` (change platform as needed)
5. *(optional)* Update translations generator.
    - Download from latest Swift 3 release [on Github](https://github.com/nodes-ios/nstack-translations-generator/releases), do NOT add to Xcode
    - Remove any old translations generator and templates present in project
6. Open `YourProject.xcodeproj` in Xcode 8 and run Swift migrator.
    - Go through suggested changes to double check
7. Go to Build Phases and modify current run scripts.
    - Update translations script as per [README](https://github.com/nodes-ios/nstack-translations-generator)
    - Add or update script checking for TODO & FIXME ([gist here](https://gist.github.com/nickskull/2df890a021ada999bda383b8413c9473))
    - Add or update Carthage copy frameworks script with new names/frameworks
8. Update build settings.
    - Enable whole module optimizations for release/adhoc
    - Enable bitcode if possible
    - Remove unused/old user-defined build settings (scroll to the bottom of build settings)
9. Build and fix errors, rinse & repeat until project compiles. 😬
    - **Alamofire** ([official migration guide](https://github.com/Alamofire/Alamofire/blob/master/Documentation/Alamofire%204.0%20Migration%20Guide.md))
	    - Change `Manager` to `SessionManager`
	    - Update completion type to `DataResponse`
	    - Rename completion closure paramter to response instead of result
	    - Requests have to start with the url, followed by method and other parameters
	    - Switch on `response.result` instead of result
	    - Update switch cases to `.success(let data)` and `.failure(let error)`
    - **Serpent**
	    - Replace `import Serializable` with `import Serpent`
	    - Remove `completionHandler:` named parameter in Alamofire requests
	    - (**important**) Set default unwrapper, or manually specify per request
    - **Blobfish**
	    - Completely replace ErrorHandler or add error handling if not present
	    - Properly setup blobs for token expired, connection error, unknown error
    - **NStackSDK**
	    - Replace `import NStack` with `import NStackSDK`
	    - Start function now takes also a `launchOptions:` parameter
    - and more *(read documentation of frameworks)*
    - *(optional)* Refactor code to newer standards along the way (small changes)
10. Fix as many (ideally all) warnings in the project, so that it's clean and updated. 
11. *(optional)* If using HockeySDK, add `NSPhotoLibraryUsageDescription` to the `Info.plist`.
12. Add or udpate README.
    - Change Swift / Xcode versions
    - Small project description
    - Things to watch out for
    - Add test users if necessary 
13. *(optional)* Implement CI, if applicable (refer [here](https://github.com/nodes-projects/ci-test-ios)).
14. After you're done open a pull request to `develop` branch.
	- Make sure that CI / other checks pass and someone does code-review
	- After it gets merged, delete the feature branch
	- If this is a framework, also open a PR to `master`  
	  (don't do this on projects if not ready for release)
15. Enjoy life and pat yourself on the back for succeeding at this. 🎉

### Swift 3 → Swift 4

Coming late 2017.
