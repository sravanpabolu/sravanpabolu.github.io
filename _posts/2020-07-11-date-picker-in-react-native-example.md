---
title: Using DateTime picker in React Native - POC
tags:

    - react
    - react-native
    - POC

---

**An Example:**

I am going to use `react-native-modal-datetime-picker` component in this example. I am using version `8.7.1` and the github link for the repo is [github](https://github.com/mmazzarolo/react-native-modal-datetime-picker)

After you create react native project, install the following package using command <br>

 `npm i react-native-modal-datetime-picker @react-native-community/datetimepicker`
 
 
Create a new file named `DatePicker.jsx` and paste the following code 

    import React, { useState } from "react";
    import { View, Image, TouchableOpacity } from "react-native";
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
                <TouchableOpacity onPress={showDatePicker}>
                    <Text> Show Date </Text>
                </TouchableOpacity>
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

Next, Add the following code above `render()` method <br>
{% highlight javascript %}
    const [aDate, setDate] = useState(new Date());

    dateCallback = (selectedDate) => {
        const currentDate = selectedDate || aDate;
        this.state.date = currentDate ;
        console.log("Selected date => " + currentDate)
    }
{% endhighlight %}

Atlast, Add the following code in `render()` method
{% highlight javascript %}
    <DatePicker selectedDateCallback={this.dateCallback} />
{% endhighlight %}
