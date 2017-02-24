# My little JS snippets

http://www.w3resource.com/javascript-exercises/javascript-basic-exercises.php

#1. Display Date & Time
    // Today is : Friday. 
    // Current time is : 4 PM : 50 : 22   

```js
    var days = ["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"];
    var a = new Date();

    var hour = a.getHours();

    console.log("Today is : " + days[a.getDay()]);
    console.log("Current time is : " + getH(hour) + " " + a.getMinutes() + ":" + a.getSeconds());


    function getH(h){
        var hours = h;
        if (hours > 12){
            return ((hours - 12) + " PM");
        } else {
            return ((12 - hours) + " AM");
        }
    }
```
