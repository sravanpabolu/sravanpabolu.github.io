---
layout: defaults/post
title: 
date: 2021-02-20 12:27
category: 
author: 
tags: [iOS, Swift, gist, Error Handling]
summary: An example for error handling in swift 
---

#### Error Handling 
Here is simple example how to use error handling in swift. 

    import UIKit

    var str = "Hello, playground"

    struct Auth{
        func authenticateUser(username: String) -> Bool {
            return username.uppercased() == "PSLV" ? true : false
        }
        
        func verifyUser(username: String) throws -> Bool{
            return username.uppercased() == "PSLV" ? true : false
        }
    }

    let user1 = Auth()
    user1.authenticateUser(username: "slv") //false
    user1.authenticateUser(username: "PSLV") //true

    try user1.verifyUser(username: "slv") //false
    try user1.verifyUser(username: "pslv") //true

    do {
        try user1.verifyUser(username: "SLV") //false
    } catch  {
        print("username wrong")
    }

    do {
        try user1.verifyUser(username: "pSLV") //true
    } catch  {
        print("username wrong")
    }

