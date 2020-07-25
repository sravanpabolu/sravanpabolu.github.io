---
layout: defaults/post
narrow: true
title: Firebase - Add value to database
tags:
    - react
    - react-native
    - Example
    - Firebase
---

_In this blog post, We'll learn, how to use push method to add a value to realtime database in Firebase. This is an example written in react/react-native application_

In this Example, we will be using 
1. React 
1. Firebase


### Prerequisite
1. Expecting that you have created a project ready in firebase and 
1. You have integrated the firebase config file in your `react` or `react-native` application.

<br>
### Getting Started
Add the following code to push an item `Buy Groceries` and the status of the item(completed/not completed) as `false` <br>

{% highlight javascript %}
    database.ref('/todoitems').push({
      done: false,
      todoItemName: "Buy Groceries"
    });
{% endhighlight %}
  
When you add item, then your JSON in Firebase DB should look like this

![TODO_Firebase_Push](/assets/images/TODO_Firebase_Push.png){: height="50%" width="50%"} 

In the next post, we will discuss on updating the data, setting `done` item to `true`. 