---
layout: defaults/post
title: Property Wrappers in Swift
date: 2021-02-03 19:57
category: 
author: 
tags: [Swift, iOS, Property Wrappers, Interviews]
summary: 
---
##### Definition
Property wrappers is definitely one of the most exciting new features in Swift 5.1. Like the name implies, a property wrapper is essentially a type that wraps a given value in order to attach additional logic to it — and can be implemented using either a struct or a class by annotating it with the @propertyWrapper attribute. Besides that, the only real requirement is that each property wrapper type should contain a stored property called wrappedValue, which tells Swift which underlying value that’s being wrapped.


##### References
1. [swiftbysundell](https://www.swiftbysundell.com/articles/property-wrappers-in-swift/)
1. 