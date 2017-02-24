# My little JS snippets

##1. Display Date & Time
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
##2. Write a JavaScript program to print the contents of the current window.  

```js
    window.print();
```
##3. JavaScript Closures Example
    // console.log(sum(2,3));   // Outputs 5 
    // console.log(sum(2)(3));  // Outputs 5 

```js
function sum(x){
    if (arguments.length == 2){
       return arguments[0] + arguments[1];
    } else {
        return function (y) {
            return x + y;
        }
    }
}
```
##4. The following function will return true if str is a palindrome; otherwise, it returns false.
    // isPalindrome("level");   // Outputs true 
    // isPalindrome("levels");   // Outputs false
    // isPalindrome("A car, a man, a maraca");   // Outputs true 

```js
function isPalindrome(str) {
    // We will replace any non-word character with empty place. 
    // Lowercase all string
    str = str.replace(/\W/g, '').toLowerCase();
    
    // First use split in order to convert string to array, every single character is different array instance.
    // Reverse the array. Use join to convert array into string.
    console.log(str == str.split('').reverse().join(''));
}
```
##5. Function isInteger(x) that determines if x is an integer.
    // isInteger(3);   // Outputs true 
    // isInteger("5");   // Outputs false
    // isInteger("car");   // Outputs false 

```js
function isInteger(x) { 
    // ^ stands for XOR so every integer with (4^0) will give integer itself. Every string will give 0
    return (x^0) === x; 
} 
```
##6. Function will output the value of factorial.
    // f(0);   // Outputs 0
    // f(5);   // Outputs 120

```js
function f(n) {
    return ((n > 1) ? n * f(n-1) : n)
}
```

