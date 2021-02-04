---
layout: defaults/post
title: Associated Types
date: 2021-02-04 12:03
category: 
author: 
tags: [iOS, Swift, Associated Types, Interviews]
summary: 
---


##### Definition
1. Associated types are a powerful way of making protocols generic, but they can be a bit confusing at first. In essence, they mark holes in protocols that must be filled by whatever types conform to those protocols.
1. Associated types work like generics.

##### Example
    protocol ItemStoring {
        associatedtype DataType

        var items: [DataType] { get set}
        mutating func add(item: DataType)
    }

    extension ItemStoring {
        mutating func add(item: DataType) {
            items.append(item)
        }
    }
    
We can create a NameDatabase struct that conforms to the ItemStoring protocol like this

    struct NameDatabase: ItemStoring {
        var items = [String]()
    }

Swift is smart enough to realize that String is being used to fill the hole in the associated type, because the items array must be whatever DataType is.

##### Usage
    var names = NameDatabase()
    names.add(item: "Siva Mani")
    names.add(item: "Mani Siva")
    print("Names: \(names.items)")

    var mobileNumbers = MobileNumbersDatabase()
    mobileNumbers.add(item: 9848022338)
    mobileNumbers.add(item: 2233898480)
    print("Mobile Numbers: \(mobileNumbers.items)")

##### Output
    Names: ["Siva Mani", "Mani Siva"]
    Mobile Numbers: [9848022338, 2233898480]

##### References
1. [hackingwithswift](https://www.hackingwithswift.com/example-code/language/what-is-a-protocol-associated-type)
1. [medium - Swift Associated Type Design Patterns](https://medium.com/@bobgodwinx/swift-associated-type-design-patterns-6c56c5b0a73a)