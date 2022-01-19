---
layout: defaults/post
title: protocol oriented programming
date: 2021-02-03 00:40
category: 
author: 
tags: [iOS, Swift, Protocol Oriented Programming, OOPs, Interviews]
summary: 
---

##### Quick Reference
1. Protocols are used to define a “blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality.
1. Protocols allow developers to write flexible and extensible code in Swift without having to compromise the language’s expressiveness.

##### Protocol Extensions vs. Base Classes
1. Since classes, structures and, enums can conform to more than one protocol, they can take the default implementation of multiple protocols. This is conceptually similar to multiple inheritance in other languages.
1. Protocols can be adopted by classes, structures, and enums, whereas base classes and inheritance are available for classes only.

##### Why POP?
1. Protocols allow you to group similar methods, functions and properties.
1. An advantage of protocols in Swift is that objects can conform to multiple protocols.
1. When writing an app this way, your code becomes more modular. Think of protocols as building blocks of functionality. When you add new functionality by conforming an object to a protocol, you don’t build a whole new object. That’s time-consuming. Instead, you add different building blocks until your object is ready.
1. Using protocols, you can define functional components and have any relevant object conform to them.
1. There is no practical difference between the two: both can place functionality into objects, use access control to limit where that functionality can be called, make one class inherit from another, and more.
1. The only real difference between the two is that in protocol-oriented programming (POP) we prefer to build functionality by composing protocols (“this new struct conforms to protocols X, Y, and Z”), whereas in object-oriented programming (OOP) we prefer to build functionality through class inheritance. However, even that is dubious because OOP developers also usually prefer composing functionality to inheriting it – it’s just easier to maintain.
1. In fact, the only important difference between the two is one of mindset: POP developers lean heavily on the protocol extension functionality of Swift to build types that get a lot of their behavior from protocols. This makes it easier to share functionality across many types, which in turn lets us build bigger, more powerful software without having to write so much code.
1. Protocol extensions allow us to provide default implementation of protocol methods and default values of protocol properties, thereby making them “optional”. Types that conform to a protocol can provide their own implementations or use the default ones.
1. If you’re coming from a more traditional object-oriented system where inheritance is more common, try to think as your first protocol as being a base class. You can then create new protocols by inheriting from that initial protocol, and write extensions so they have default implementations. However, a better approach is to write lots of small protocols that each do specific, individual things: one to make products purchasable, one to make them serializable, one to make them searchable, and so on. You can then add default implementations to those extensions, which means you can add functionality to existing types just by making them conform to your protocol.

##### Example

    protocol Queue {
        var count: Int { get }
        mutating func push(_ element: Int) 
        mutating func pop() -> Int
    }

##### Implementation/Confirming a Protocol
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
    
##### The Pillars of POP
**Protocol Extensions**<br>
Protocols serve as blueprints: they tell us what adopters shall implement, but you can’t provide implementation within a protocol. What if we need to define default behavior for conforming types? We need to implement it in a base class, right? Wrong! Having to rely on a base class for default implementation would eclipse the benefits of protocols. Besides, that would not work for value types. Luckily, there is another way: protocol extensions are the way to go! In Swift, you can extend a protocol and provide default implementation for methods, computed properties, subscripts and convenience initializers. In the following example, I provided default implementation for the type method uid().

    extension Entity {
        static func uid() -> String {
            return UUID().uuidString
        }
    }

Now types that adopt the protocol need not implement the uid() method anymore.

    struct Order: Entity {
        var name: String
        let uid: String = Order.uid()
    }
    let order = Order(name: "My Order")
    print(order.uid)
    // 4812B485-3965-443B-A76D-72986B0A4FF4

**Protocol Inheritance**<br>
A protocol can inherit from other protocols and then add further requirements on top of the requirements it inherits. In the following example, the protocol Persistable inherits from the Entity protocol I introduced earlier. It adds the requirement to save an entity to file and load it based on its unique identifier.

    protocol Persistable: Entity {
        func write(instance: Entity, to filePath: String)
        init?(by uid: String)
    }

The types that adopt the Persistable protocol must satisfy the requirements defined in both the Entity and the Persistable protocol.

If your type requires persistence capabilities, it should implement the Persistable protocol.

    struct PersistableEntity: Persistable {
        var name: String
        func write(instance: Entity, to filePath: String) { // ...
        }  
        init?(by uid: String) {
            // try to load from the filesystem based on id
        }
    }

Whereas types that do not need to be persisted shall only implement the Entity protocol:

    struct InMemoryEntity: Entity {
        var name: String
    }

Protocol inheritance is a powerful feature which allows for more granular and flexible designs.

**Protocol Composition**<br>
Swift does not allow multiple inheritance for classes. However, Swift types can adopt multiple protocols. Sometimes you may find this feature useful.
Here’s an example: let’s assume that we need a type which represents an Entity.
We also need to compare instances of given type. And we want to provide a custom description, too.

We have three protocols which define the mentioned requirements:
- Entity
- Equatable
- CustomStringConvertible
<br>
If these were base classes, we’d have to merge the functionality into one superclass; however, with POP and protocol composition, the solution becomes:
       
       struct MyEntity: Entity, Equatable, CustomStringConvertible {
            var name: String
            // Equatable
            public static func ==(lhs: MyEntity, rhs: MyEntity) -> Bool {
                return lhs.name == rhs.name
            }
            // CustomStringConvertible
            public var description: String {
                return "MyEntity: \(name)"
            }
        }
        let entity1 = MyEntity(name: "42")
        print(entity1)
        let entity2 = MyEntity(name: "42")
        assert(entity1 == entity2, "Entities shall be equal")

This design not only is more flexible than squeezing all the required functionality into a monolithic base class but also works for value types.


##### References
1. [raywenderlich](https://www.raywenderlich.com/6742901-protocol-oriented-programming-tutorial-in-swift-5-1-getting-started)
1. [hackingwithswift](https://www.hackingwithswift.com/quick-start/understanding-swift/how-is-protocol-oriented-programming-different-from-object-oriented-programming)
1. [hackingwithswift](https://www.hackingwithswift.com/example-code/language/what-is-protocol-oriented-programming)
1. [toptal](https://www.toptal.com/swift/introduction-protocol-oriented-programming-swift)
1. [pluralsight](https://www.pluralsight.com/guides/protocol-oriented-programming-in-swift)
