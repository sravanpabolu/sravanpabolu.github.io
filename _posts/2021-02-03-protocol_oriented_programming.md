---
layout: defaults/post
title: protocol oriented programming
date: 2021-02-03 00:40
category: 
author: 
tags: [iOS, Swift, Protocol Oriented Programming, OOPs]
summary: 
---

##### Quick Reference
1. Protocols are used to define a “blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality.
1. Protocols allow developers to write flexible and extensible code in Swift without having to compromise the language’s expressiveness.

### Protocol Extensions vs. Base Classes
1. Since classes, structures and, enums can conform to more than one protocol, they can take the default implementation of multiple protocols. This is conceptually similar to multiple inheritance in other languages.
1. Protocols can be adopted by classes, structures, and enums, whereas base classes and inheritance are available for classes only.

### Why POP?
1. Protocols allow you to group similar methods, functions and properties.
1. An advantage of protocols in Swift is that objects can conform to multiple protocols.
1. When writing an app this way, your code becomes more modular. Think of protocols as building blocks of functionality. When you add new functionality by conforming an object to a protocol, you don’t build a whole new object. That’s time-consuming. Instead, you add different building blocks until your object is ready.
1. Using protocols, you can define functional components and have any relevant object conform to them.
1. There is no practical difference between the two: both can place functionality into objects, use access control to limit where that functionality can be called, make one class inherit from another, and more.
1. The only real difference between the two is that in protocol-oriented programming (POP) we prefer to build functionality by composing protocols (“this new struct conforms to protocols X, Y, and Z”), whereas in object-oriented programming (OOP) we prefer to build functionality through class inheritance. However, even that is dubious because OOP developers also usually prefer composing functionality to inheriting it – it’s just easier to maintain.
1. In fact, the only important difference between the two is one of mindset: POP developers lean heavily on the protocol extension functionality of Swift to build types that get a lot of their behavior from protocols. This makes it easier to share functionality across many types, which in turn lets us build bigger, more powerful software without having to write so much code.
1. Protocol extensions allow us to provide default implementation of protocol methods and default values of protocol properties, thereby making them “optional”. Types that conform to a protocol can provide their own implementations or use the default ones.
1. If you’re coming from a more traditional object-oriented system where inheritance is more common, try to think as your first protocol as being a base class. You can then create new protocols by inheriting from that initial protocol, and write extensions so they have default implementations. However, a better approach is to write lots of small protocols that each do specific, individual things: one to make products purchasable, one to make them serializable, one to make them searchable, and so on. You can then add default implementations to those extensions, which means you can add functionality to existing types just by making them conform to your protocol.

## Example
### Definition
    protocol Queue {
        var count: Int { get }
        mutating func push(_ element: Int) 
        mutating func pop() -> Int
    }

### Implementation/Confirming a Protocol
    struct Container: Queue {
        private var items: [Int] = []
        
        var count: Int {
            return items.count
        }
        
        mutating func push(_ element: Int) {
            items.append(element)
        }
        
        mutating func pop() -> Int {
            return items.removeFirst()
        }
    }


## References
1. [raywenderlich](https://www.raywenderlich.com/6742901-protocol-oriented-programming-tutorial-in-swift-5-1-getting-started)
1. [hackingwithswift](https://www.hackingwithswift.com/quick-start/understanding-swift/how-is-protocol-oriented-programming-different-from-object-oriented-programming)
1. [hackingwithswift](https://www.hackingwithswift.com/example-code/language/what-is-protocol-oriented-programming)
1. [toptal](https://www.toptal.com/swift/introduction-protocol-oriented-programming-swift)
