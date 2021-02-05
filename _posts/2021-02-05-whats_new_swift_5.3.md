---
layout: defaults/post
title: 
date: 2021-02-05 17:48
category: 
author: 
tags: [Swift 5.3, Interviews]
summary: 
---

##### Swift 5.3 Features
1. Multi-pattern catch clauses

        enum TemperatureError: Error {
            case tooCold, tooHot
        }
1. Multiple trailing closures

        var body: some View {
            Button(action: {
                self.showOptions.toggle()
            }) {
                Image(systemName: "gear")
            }
        }
    ///Can now be written as this:
        var body: some View {
            Button {
                self.showOptions.toggle()
            } label: {
                Image(systemName: "gear")
            }
        }
        
1. Synthesized Comparable conformance for enums
    
        enum Size: Comparable {
            case small
            case medium
            case large
            case extraLarge
        }
        
        let shirtSize = Size.small
        let personSize = Size.large
            
        if shirtSize < personSize {
            print("That shirt is too small")
        }

1. self is no longer required in many places
    Example: inside closure. 

1. Type-Based Program Entry Points
1. where clauses on contextually generic declarations
1. Enum cases as protocol witnesses
1. Refined didSet Semantics
1. A new Float16 type
1. Swift Package Manager gains binary dependencies, resources, and  more