---
layout: defaults/post
title: dispatchQueue vs dispatchSemaphore
date: 2021-02-02 19:49
category: 
author: Sravan Kumar Pabolu
tags: [iOS, DispatchQueue, DispatchSemaphore, Interview Preparation]
summary: We are discussing about the difference between DispatchQueue and DispatchSemaphore in iOS
narrow: true
---

# Theory

##### Definition 
Semaphores and groups have, in a sense, opposite semantics. Both maintain a count. With a semaphore, a wait is allowed to proceed when the count is non-zero. With a group, a wait is allowed to proceed when the count is zero.

A semaphore is useful when you want to set a maximum on the number of threads operating on some shared resource at a time. One common use is when the maximum is 1 because the shared resource requires exclusive access.

A group is useful when you need to know when a bunch of tasks have all been completed.
[Reference](https://stackoverflow.com/a/49924767/1918002)

##### Simple words 
Use a semaphore to limit the amount of concurrent work at a given time. Use a group to wait for any number of concurrent work to finish execution.

[Reference](https://stackoverflow.com/a/49924716/1918002)

##### Example

Execute the following in a playground.

    func performUsingGroup() {
        let dq1 = DispatchQueue.global(qos: .default)
        let dq2 = DispatchQueue.global(qos: .default)
        let group = DispatchGroup()

        for i in 1...3 {
            group.enter()
            dq1.async {
                print("\(#function) DispatchQueue 1: \(i)")
                group.leave()
            }
        }
        for i in 1...3 {
            group.enter()
            dq2.async {
                print("\(#function) DispatchQueue 2: \(i)")
                group.leave()
            }
        }

        group.notify(queue: DispatchQueue.main) {
            print("done by group")
        }
    }

    func performUsingSemaphore() {
        let dq1 = DispatchQueue.global(qos: .default)
        let dq2 = DispatchQueue.global(qos: .default)
        let semaphore = DispatchSemaphore(value: 1)

        for i in 1...3 {
            dq1.async {
                _ = semaphore.wait(timeout: DispatchTime.distantFuture)
                print("\(#function) DispatchQueue 1: \(i)")
                semaphore.signal()
            }
        }
        for i in 1...3 {
            dq2.async {
                _ = semaphore.wait(timeout: DispatchTime.distantFuture)
                print("\(#function) DispatchQueue 2: \(i)")
                semaphore.signal()
            }
        }
    }

    performUsingGroup()
    print("=============")
    performUsingSemaphore()

##### Output

    performUsingGroup() DispatchQueue 1: 1
    performUsingGroup() DispatchQueue 1: 2
    performUsingGroup() DispatchQueue 2: 1
    performUsingGroup() DispatchQueue 1: 3
    performUsingGroup() DispatchQueue 2: 2
    performUsingGroup() DispatchQueue 2: 3
    =============
    performUsingSemaphore() DispatchQueue 1: 1
    performUsingSemaphore() DispatchQueue 1: 2
    performUsingSemaphore() DispatchQueue 1: 3
    performUsingSemaphore() DispatchQueue 2: 1
    performUsingSemaphore() DispatchQueue 2: 2
    performUsingSemaphore() DispatchQueue 2: 3
    done by group
