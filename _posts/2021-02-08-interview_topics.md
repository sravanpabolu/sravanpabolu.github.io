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
