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
    return ((hours == 24) ? (0 + " AM"):((hours - 12) + " PM"));
  } else {
    return ((hours == 0) ? (0 + " PM"):((12 - hours) + " AM"));
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
        // In functions arguments received as array. 
        // We need to check if their is two or one argument in array. 
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
    
    // First use split in order to convert string to array.
    // So, every single character is different array instance.
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
    // ? stands for if statement - if n = 1 or less will return - n. if n > 1, then n * f(n-1)
    // f(n); is recursion function
    return ((n > 1) ? n * f(n-1) : n)
}
```
##7. Call / Apply / Bind functions examples.
     Generally speaking: stabilizing the "this" keyword.
```js
var person = {hi: "Hello"};

function showFullName(pep) {
    console.log (this.hi);
}

showFullName.call(person); 
// Output: Hello

// ------------

var mike = {
   checkThis: function() {
       function checkOther(){
           console.log(this);
       }
        checkOther.call(this)
    }
}

mike.checkThis();
// Output: mike Object

// ------------

function a(b,c,d){
    console.log(this);
    console.log(b);
    console.log(c);
    console.log(d);
}

a.call(1,2,3,4); 
// this = 1

a.apply(1, [2,3,4]);
// this = 1
// apply function need to passing in an array of parameters - this only difference with call function.
// So, both methods "a.call(1,2,3,4);" and "a.apply(1, [2,3,4]);" are equivalent with same output.

a(1,2,3,4); 
// this = window object

// ------------

function sum(){
    var total = 0;
    for (var i = 0; i <arguments.length; i++){
        total += arguments[i];
    }
    return total;
}

var x = sum.call(null, 1,2,3);
// Output: 6

var thing = [1,2,3];

var x = sum.apply(null, thing);

// Output: 6

// ------------

"use strict";
var a = function(){
    console.log(this);
}.bind(2);

a();

// Output: undefined

// Inside bind fucntion, we actually defining "this" keyword paraemter
"use strict";
var a = function(){
    console.log(this);
}.bind(2);

a();

// Output: 2

// Just another way of binding
"use strict";
function a(){
    console.log(this);
};

var f = a.bind(2);
f();

// Output: 2
```
