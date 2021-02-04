---
layout: defaults/post
title: SOLID Principles
date: 2021-02-04 12:11
category: 
author: 
tags: [Interviews, SOLID Principles]
summary: 
---

#### Concepts
##### Single-responsibility principle
A class should only have a single responsibility, that is, only changes to one part of the software's specification should be able to affect the specification of the class.

##### Open–closed principle
"Software entities ... should be open for extension, but closed for modification."
##### Liskov substitution principle
"Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program." 

##### Interface segregation principle
"Many client-specific interfaces are better than one general-purpose interface."

##### Dependency inversion principle
One should "depend upon abstractions, [not] concretions."
<BR>
<HR>
<BR>
#### Details
##### S - Single Responsibility Principle — SRP

This principle states that a class should do only one job! Yes this is the meaning of single responsibility and there is no need to sugar coat it. “A class = performs one operation” simple and stupid.

    protocol SwitchOn {
        func on()
    }

    protocol SwitchOff {
        func off()
    }

    class Switch: SwitchOn, SwitchOff {
        private var state: Bool = false

        func on() {
            state = true
        }

        func off() {
            state = false
        }

        var description: String {
            return state ? "Switched On" : "Switched Off"
        }
    }

    let aSwitch = Switch() /// Represents your model
    aSwitch.off()
    aSwitch.on()

While the above code is totally correct but it is “anti-pattern”. For us to be cohesive we need to perform these actions based on the given contract, which is through the Interface and not directly accessing the Concrete Type.

Refactoring the code
    
    /// Conforms to `Executable`
    class TurnOn: Executable {

        private let  aSwitch: SwitchOn

        init(aSwitch: SwitchOn) {
            self.aSwitch = aSwitch
        }

        func execute() {
            //Single Responsibility
            self.aSwitch.on()
        }
    }
    /// Conforms to `Executable`
    class TurnOff: Executable {
        private let  aSwitch: SwitchOff

        init(aSwitch: SwitchOff) {
            self.aSwitch = aSwitch
        }

        func execute() {
            //Single Responsibility
            self.aSwitch.off()
        }
    }

<BR>
<HR>
<BR>

##### O - Open/Closed Principle

In object-oriented programming, the open–closed principle states "software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification"; that is, such an entity can allow its behaviour to be extended without modifying its source code.


The Open Closed principle enforces a rule that a class can be easily extended but at the same time forbids any modification to it’s self. This principle highly draws it’s traits from the Decorator & Strategy pattern. The Decorator allows extension of behaviour dynamically or statically during runtime. It is often referred to as “the alternative to subclassing”, while the Strategy allows implementation of different algorithms interchangeable within the same family.

    //MARK: Extension for interchangeable algorithms
    extension Developer where Self: IOSEngineer {
        func traits() -> String { return iosTraits }
    }

    extension Developer where Self == WebProgrammer {
        func traits() -> String {
            return "We are cool and we do both \(self.language) and CSS also."
        }
    }

<BR>
<HR>
<BR>

##### L - Liskov substitution principle 
Liskov substitution principle states that all derived class should be substitutable for it’s original base class. What this means in practice is that a subclass should always be interchangeable for it’s super class. The main purpose of this principle is to guarantee semantic interoperability within the types hierarchy.

    class Vehicle {
        let name: String
        let speed: Double
        let wheels: Int

        init(name: String, speed: Double, wheels: Int) {
            self.name = name
            self.speed = speed
            self.wheels = wheels
        }

        func canfly() -> Bool {
            return false
        }
    }

    /// Airplane is a subclass of Vehicle
    class Airplane: Vehicle {
        override func canfly() -> Bool {
            return true
        }
    }

    /// Car is derived from Vehicle. 
    class Car: Vehicle { }

    class Handler {
        static func speedDescription(for vehicle: Vehicle) -> String {
            ///Vehicle could be an Airplane or Car 
            ///This is substitutability or interchaneable
            if vehicle.canfly() {
                return "It flys at \(vehicle.speed) knot "
            } else {
                return "Runs at \(vehicle.speed) kph"
            }
        }
    }

Liskov Substitution guarantees that our speedDescription algorithm will keep functioning regardless of which Subclass Type it receives as an argument. This term is known as semantic interoperability.

    let car = Car(name: "BMW", speed: 180.00, wheels: 4)
    let plane = Airplane(name: "KLM", speed: 34.00, wheels: 3)

    ///Based on Liskov Handler should always be able to
    ///Process speedDescription when given any type of Vehicle

    let carSpeedDescription = Handler.speedDescription(for: car)
    let planeSpeedDescription = Handler.speedDescription(for: plane)

<BR>
<HR>
<BR>

##### I — Interface Segregation  
The Interface Segregation Principle deals separation of concerns. It states that a client should not be forced to implement or depend upon methods that it does not use. It is better to have many specific interfaces than to have a monolithic general purpose interface. The entire purpose of Interface Segregation is to reduce interface bloat or what is known as interface pollution and to favour code readability.


<BR>
<HR>
<BR>

##### D - Dependency Inversion Principle
Dependency Inversion Principle states that, higher level modules shouldn’t depend on the lower level modules, they should both depend on abstractions. In other words all entities should be based on Abstract Interfaces and not on Concrete Types. The principle also stressed that abstractions should not depend on details. Details should depend upon abstractions.

##### Example 
1. Remote file server client


<BR>
<HR>
<BR>
##### References
1. [medium - part 1](https://medium.com/@bobgodwinx/solid-principles-part-1-f3d11b3159f0)
1. [medium - part 2](https://medium.com/@bobgodwinx/solid-principles-part-2-a22d4c8ed906)
1. [medium - part 3](https://medium.com/@bobgodwinx/solid-principles-part-3-43aad943b056)
1. [medium - part 4](https://medium.com/@bobgodwinx/solid-principles-part-4-13de4d4d7571)
1. [medium - part 5](https://medium.com/@bobgodwinx/solid-principles-part-5-b1d2047c2d55)
1. [Wiki](https://en.wikipedia.org/wiki/SOLID)