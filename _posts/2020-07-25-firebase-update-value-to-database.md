---
layout: defaults/post
narrow: true
title: Firebase - Update value to database
tags:

    - react
    - react-native
    - Example
    - Firebase

---

_In this blog post, We'll learn, how to use update method to update a value to realtime database in Firebase. This is an example written in react/react-native application_

In this Example, we will be using 

1. React 
1. Firebase

### Prerequisite

1. Expecting that you have created a project ready in firebase and 
1. You have integrated the firebase config file in your `react` or `react-native` application.

<br>

### Getting Started

Add the following code to update an item `Buy Groceries` and the status of the item to __completed__ as `true` <br>

{% highlight javascript %}

    database.ref('/todoitems').update({
      [id]: {
        todoItemName: "Buy Groceries",
        done: true
      }
    })

{% endhighlight %}

