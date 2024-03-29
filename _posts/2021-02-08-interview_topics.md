---
layout: defaults/post
title: iOS Interview Quick Reference
date: 2021-02-08 19:41
category: 
author: 
tags: [iOS, Interviews]
summary: 
---

### Quick Reference
Here are few quick reference for interview preparation

## iOS
1. App States <BR>
    `Not Running > Inactive > Active > Background > Suspended`
1. UIButton Hierarchy <br>
    `UIButton > UIControl > UIView > UIResponder > NSObject`
1. AppDelegate lifecycle
    1. application:willFinishLaunchingWithOptions
    1. application:didFinishLaunchingWithOptions
    1. applicationDidBecomeActive
    1. applicationWillResignActive
    1. applicationDidEnterBackground
    1. applicationWillEnterForeground
    1. applicationWillTerminate
1. UIViewController lifecycle
    1. Initialization
        1. instantiateViewController(withIdentifier:) - From Storyboard
        1. init(nibName:bundle:) - From NIB/XIB file
        1. loadView() - Specify the views for a view controller using the loadView() method. In that method, create your view hierarchy programmatically and assign the root view of that hierarchy to the view controller’s view property.
1. UIView
    1. Initialization 
        1. init(frame:) - load view programatically
        1. init(coder:) - if you need to load view from storyboards/nib files
1. Autolayout 
    1. Constraints - Adjust the size and position of the view using Auto Layout constraints.
    1. Attach Auto Layout constraints to one of the view's anchors.
    1. translatesAutoresizingMaskIntoConstraints - A Boolean value that determines whether the view’s autoresizing mask is translated into Auto Layout constraints.
1. URLSession Configuration Types
    1. default - A default session behaves much like the shared session, but lets you configure it. You can also assign a delegate to the default session to obtain data incrementally.
    1. Ephemeral - Ephemeral sessions are similar to shared sessions, but don’t write caches, cookies, or credentials to disk.
    1. background - Background sessions let you perform uploads and downloads of content in the background while your app isn't running.
1. URLSession Tasks
    1. dataTask - Data tasks send and receive data using NSData objects. Data tasks are intended for short, often interactive requests to a server.
    1. downloadTask - Download tasks retrieve data in the form of a file, and support background downloads and uploads while the app isn’t running.
    1. uploadTask - Upload tasks are similar to data tasks, but they also send data (often in the form of a file), and support background uploads while the app isn’t running.
    1. streamTask
    1. webSocketTask - WebSocket tasks exchange messages over TCP and TLS, using the WebSocket protocol.
1. Dispatch - also know as Grand Central Dispatch
    1. DispatchQueue - object that manages the execution of tasks serially/concurently on main/background thread
    1. DispatchWorkItem - the work you want to perform, encapsulated in a way that lets you attach a completion handle
    1. DispatchGroup - group of tasks that you monitor as a single unit
        1. enter()
        1. leave()
        1. wait()
        1. notify() 
    1. Workloop - A dispatch object that prioritizes the execution of tasks based on their quality-of-service (QoS) level.
        1. userInteractive - highest priority - animations, event handing, etc.,
        1. userInitiated - qos class for tasks that prevent user from actively using your app.
        1. default - default
        1. utility - qos class for tasks that the user doesnot track actively
        1. background - qos class for maintainance/cleanup tasks 
        1. unspecified - absense of qos
    1. DispatchSemaphore - An object that controls access to a resource across multiple execution contexts through use of a traditional counting semaphore.
        1. signal() - Signals (increments) a semaphore.
        1. wait() - Waits for, or decrements, a semaphore.
1. NSOperation - An abstract class that represents the code and data associated with a single task.
1. Closures
    1. escaping - A closure is said to escape a function when the closure is passed as an argument to the function, but is called after the function returns. When you declare a function that takes a closure as one of its parameters, you can write @escaping before the parameter’s type to indicate that the closure is allowed to escape.
### Memory Management
1. Autoreleasepool:
    Here’s how autorelease works. Your code runs in the presence of something called an autorelease pool. (If you look in main.m, you can actually see an autorelease pool being created.) When you send autorelease to an object, that object is placed in the autorelease pool, and a number is incremented saying how many times this object has been placed in this autorelease pool. From time to time, when nothing else is going on, the autorelease pool is automatically drained. This means that the autorelease pool sends release to each of its objects, the same number of times as that object was placed in this autorelease pool, and empties itself of all objects. If that causes an object’s retain count to be zero, fine; the object is destroyed in the usual way. So autorelease is just like release — effectively, it is a form of release — but with a proviso, “later, not right this second.”
    <br>
    ref: [Reference](http://www.apeth.com/iOSBook/ch12.html#EXstrongWeakDance)
1. what is unowned?
    unowned is like an assign property policy in Objective-C (non-ARC weak)
    ref: [stackoverflow](https://stackoverflow.com/a/41664269/1918002)
    ref: [Apple](https://developer.apple.com/library/archive/releasenotes/ObjectiveC/RN-TransitioningToARC/Introduction/Introduction.html)
    

