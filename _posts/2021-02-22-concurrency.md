---
layout: defaults/post
title: 
date: 2021-02-22 13:07
category: 
author: 
tags: [Interviews, iOS, Swift, Concurrency]
summary: 
---

#### Concurrency and Grand Central Dispatch
Concurrency lets you take advantage of the fact that your device has multiple CPU cores. To make use of these cores, you will need to use multiple threads.
However, threads are a low-level tool, and managing threads manually in an efficient manner is extremely difficult.

With GCD, Apple took an asynchronous design approach to the problem. Instead of creating threads directly, you use GCD to schedule work tasks, and the system will perform these tasks for you by making the best use of its resources. 

#### Dispatch Queues

1. The Main dispatch queue (serial, pre-defined) - UI Tasks like touch, scroll, pan, etc., 
1. Global queues (concurrent, pre-defined) - long running tasks like network call, etc., 
1. Private queues (can be serial or concurrent, you create them)

```
    URLSession.shared.dataTask(with: url) { data, response, error in
        if let data = data {
            DispatchQueue.main.async { // UI work
                self.label.text = String(data: data, encoding: .utf8)
            }
        }
    }
```

In addition to the main queue, every app comes with several pre-defined concurrent queues that have varying levels of Quality of Service 
1. userInteractive - highest priority - animations, event handing, etc.,
1. userInitiated - qos class for tasks that prevent user from actively using your app.
1. default - default
1. utility - qos class for tasks that the user doesnot track actively
1. background - qos class for maintainance/cleanup tasks 
1. unspecified - absense of qos

```
    DispatchQueue.global(qos: .background).async {
        print("we are on global background queue")
    }
```
```
    DispatchQueue.global().async {
        print("Generic global queue")
    }
```
```
    let serial = DispatchQueue(label: "com.besher.serial-queue")
    serial.async {
        print("Private serial queue")
    }
```
By default, private queues are serial. 
```    
    let concurrent = DispatchQueue(label: "com.besher.serial-queue", attributes: .concurrent)
    concurrent.sync {
        print("Private concurrent queue")
    }
```

#### Task/DispatchWorkItem
Tasks can refer to any block of code that you submit to a queue using the sync or async functions.

```
    DispatchQueue.global().async {
        print("Anonymous closure")
    }
```
OR
```
    let item = DispatchWorkItem(qos: .utility) {
        print("Work item to be executed later")
    }
```

#### Sync vs Async
When your code reaches a sync statement, it will block the current queue until that task completes. Once the task returns/completes, control is returned to the caller, and the code that follows the sync task will continue.

Think of sync as synonymous with ‘blocking’.

An async statement, on the other hand, will execute asynchronously with respect to the current queue, and immediately returns control back to the caller without waiting for the contents of the async closure to execute. There is no guarantee as to when exactly the code inside that async closure will execute.



#### References
1. [freecodecamp](https://www.freecodecamp.org/news/ios-concurrency/)
1. [medium](https://medium.com/swift-india/parallel-programming-with-swift-part-1-4-df7caac564ae)
1. 