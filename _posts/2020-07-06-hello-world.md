---
title:  XCode error - The app delegate must implement the window property
tags:
    - iOS
    - SwiftUI
    - Stack Overflow
    - XCode
---

How to resolve the error **The app delegate must implement the window property if it wants to use a main storyboard file swift**

[Stackoverflow - Issue](https://stackoverflow.com/questions/29441682/the-app-delegate-must-implement-the-window-property-if-it-wants-to-use-a-main-st/59962469)

If you are not using `SwiftUI`, Here are the steps, I have followed. 

1. Deleted `Application Scene Manifest` entry from `Info.plist`
1. Deleted `SceneDelegate.swift` file 
1. Deleted all scene related methods in `AppDelegate.swift` class
1. added `var window: UIWindow?` property in `AppDelegate.swift` class

After these steps, your `AppDelegate.swift` file should look something like the following. 

    import UIKit
    
    @UIApplicationMain
    class AppDelegate: UIResponder, UIApplicationDelegate {
    
        var window: UIWindow?
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
            // Override point for customization after application launch.
            return true
        }
    }


