---
layout: defaults/post
title: 
date: 2021-02-09 14:45
category: 
author: 
tags: [design-patterns, Interviews]
summary: 
---

##### Types of Design Patterns
There are mainly three types of design patterns: 

##### Creational 
These design patterns are all about __class instantiation or object creation__. These patterns can be further categorized into __*Class-creational patterns and object-creational patterns*__. While class-creation patterns use inheritance effectively in the instantiation process, object-creation patterns use delegation effectively to get the job done. 
Creational design patterns are the 
1. Factory Method - Protocols, 
    Factory Method pattern makes the codebase more flexible to add or remove new types. 
1. Abstract Factory, 
1. Builder,  
1. Singleton,  
1. Object Pool, and  
1. Prototype. 

##### Structural 
These design patterns are about organizing different classes and objects to form larger structures and provide new functionality. 
Structural design patterns are  
1. Adapter - Protocols,  
    The Adapter design pattern converts the interface of a class into another interface that clients expect. Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces. It decouples the client from the class of the targeted object. As an example, with the NSCopying protocol, any class can provide a standard copy method.
1. Bridge,  
1. Composite,  
1. Decorator - Category/Extensions and Delegation,  
    The Decorator pattern dynamically adds behaviors and responsibilities to an object without modifying its code. It’s an alternative to subclassing where you modify a class’s behavior by wrapping it with another object.
1. Facade - framework/library ?,  
    The Facade design pattern provides a single interface to a complex subsystem. Instead of exposing the user to a set of classes and their APIs, you only expose one simple unified API.
1. Flyweight,  
1. Private Class Data, and  
1. Proxy. 

##### Behavioral 
Behavioral patterns are about identifying common communication patterns between objects and realize these patterns. 
Behavioral patterns are   
1. Chain of responsibility,   
1. Command,   
1. Interpreter,   
1. Iterator,   
1. Mediator,   
1. Memento - Archiving, Serialization and State Restoration,
    In Memento Pattern saves your stuff somewhere. Later on, this externalized state can be restored without violating encapsulation; that is, private data remains private.
1. Null Object,   
1. Observer - Notifications and Key-Value Observing (KVO).,
    The Observer design pattern defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically. The Observer pattern is essentially a publish-and-subscribe model in which the subject and its observers are loosely coupled. Communication can take place between the observing and observed objects without either needing to know much about the other.
1. State,   
1. Strategy - Protocols (eg. different implementations can be given to the methods in different classes),   
    1. Strategy pattern allows you to change the behaviour of an algorithm at run time, without breaking the rest of your code. Using interfaces, we are able to define a family of algorithms, encapsulate each one, and make them interchangeable, allowing us to select which algorithm to execute at run time. It is a very good example of using polymorphism.
1. Template method,   
1. Visitor 

##### References
1. [geeksforgeeks](https://www.geeksforgeeks.org/design-patterns-set-1-introduction/)
1. [medium](https://chetan-aggarwal.medium.com/ios-design-patterns-f478abd78132)
1. [apple](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CocoaFundamentals/CocoaDesignPatterns/CocoaDesignPatterns.html#//apple_ref/doc/uid/TP40002974-CH6-SW43)
1. [Strategy pattern - thomashanning](http://www.thomashanning.com/the-strategy-pattern/)