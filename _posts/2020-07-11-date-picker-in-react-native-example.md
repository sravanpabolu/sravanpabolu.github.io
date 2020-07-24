---
layout: defaults/post
narrow: true
title: Using DateTime picker in React Native - example
tags:
    - react
    - react-native
    - Example
---

_In this blog post, We'll learn, how to develop a simple react native app, where user can click a button to open date picker, select a date and come back to previous screen, with the selected date displayed to a label_

In this Example, we will be using 
1. React `hooks` - inside `DatePicker` component 
1. Call backs - For getting the selected date from `DatePicker` to `App` 


### Prerequisite
I am going to use `react-native-modal-datetime-picker` npmjs module in this example. I am using version `8.7.1` and the github link for the repo is [here](https://github.com/mmazzarolo/react-native-modal-datetime-picker)

<br>
### Getting Started
Assuming that you have already created react native project, install the following package in terminal using the following command <br>

{% highlight javascript %}
    npm i react-native-modal-datetime-picker @react-native-community/datetimepicker
{% endhighlight %}
  
Create a new file named `DatePicker.jsx` and paste the following code 

    import React, { useState } from "react";
    import { View, Button } from "react-native";
    import DateTimePickerModal from "react-native-modal-datetime-picker";

    const DatePicker = ({ selectedDateCallback }) => {
        const [isDatePickerVisible, setDatePickerVisibility] = useState(false);

        const showDatePicker = () => {
            setDatePickerVisibility(true);
        };

        const hideDatePicker = () => {
            setDatePickerVisibility(false);
        };

        const handleConfirm = (date) => {
            console.log("A date has been picked: ", date);
            hideDatePicker();

            //send back to parent component
            selectedDateCallback(date);
        };

        return (
            <View>
                <Button onPress={showDatePicker} title="Show Date Picker "></Button>
                <DateTimePickerModal
                    isVisible={isDatePickerVisible}
                    mode="date"
                    onConfirm={handleConfirm}
                    onCancel={hideDatePicker}
                />
            </View>
        );
    };

    export default DatePicker;

Now, Lets come back to `App.js` <br> 
First, Add Import <br>
{% highlight javascript %}
    import DatePicker from './DatePicker'
{% endhighlight %}

Next, Add the following code above `return()` method <br>
{% highlight javascript %}
    const [aDate, setDate] = useState(new Date());

    dateCallback = (selectedDate) => {
        const currentDate = selectedDate || aDate;
        this.state.date = currentDate ;
        console.log("Selected date => " + currentDate)
    }
{% endhighlight %}

Atlast, Add the following code in `return()` method
{% highlight javascript %}
    <DatePicker selectedDateCallback={this.dateCallback} />
{% endhighlight %}

Now, Save all the changes run the app in iOS Simulator or Android emulator or your own device to see the output. You can find the source code for the project [here](https://github.com/sravanpabolu/DatePickerExampleReactNative)

Find the screenshots below: 

![ReactNativeDateTimePicker](/assets/images/ReactNativeDateTimePicker2.png){: height="50%" width="50%"} 
![ReactNativeDateTimePicker](/assets/images/ReactNativeDateTimePicker3.png){: height="50%" width="50%"} 