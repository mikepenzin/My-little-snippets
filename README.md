# My little JS snippets

See - https://gist.github.com/mikepenzin

- [1. Display Date & Time](#1-display-date--time)
- [2. Write a JavaScript program to print the contents of the current window.](#2-write-a-javascript-program-to-print-the-contents-of-the-current-window)
- [3. JavaScript Closures Example](#3-javascript-closures-example)
- [4. The following function will return true if str is a palindrome; otherwise, it returns false.](#4-the-following-function-will-return-true-if-str-is-a-palindrome-otherwise-it-returns-false)
- [5. Function isInteger(x) that determines if x is an integer.](#5-function-isintegerx-that-determines-if-x-is-an-integer)
- [6. Function will output the value of factorial. (Recursion)](#6-function-will-output-the-value-of-factorial-recursion)
- [7. Call / Apply / Bind functions examples.](#7-call--apply--bind-functions-examples)
- [8. Object creation patterns (Part 1)](#8-object-creation-patterns-part-1)
- [9. Object creation patterns (Part 2)](#9-object-creation-patterns-part-2)
- [10. The Singleton Pattern](#10-the-singleton-pattern)
- [11. Promises Patterns](#11-promises-patterns)
- [Useful Links](#useful-links)
- [Books](#books)


## 1. Display Date & Time
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
## 2. Write a JavaScript program to print the contents of the current window.  

```js
window.print();
```
## 3. JavaScript Closures Example
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
## 4. The following function will return true if str is a palindrome; otherwise, it returns false.
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
## 5. Function isInteger(x) that determines if x is an integer.
    // isInteger(3);   // Outputs true 
    // isInteger("5");   // Outputs false
    // isInteger("car");   // Outputs false 

```js
function isInteger(x) { 
    // ^ stands for XOR so every integer with (4^0) will give integer itself. Every string will give 0
    return (x^0) === x; 
} 
```
## 6. Function will output the value of factorial. (Recursion)
    // f(0);   // Outputs 0
    // f(5);   // Outputs 120

```js
function f(n) {
    // ? stands for if statement - if n = 1 or less will return - n. if n > 1, then n * f(n-1)
    // f(n); is recursion function
    return ((n > 1) ? n * f(n-1) : n)
}
```
## 7. Call / Apply / Bind functions examples.
     Generally speaking: stabilizing the "this" keyword.
```js
// 1. Call, Apply
var person = {hi: "Hello"};

function showFullName(pep) {
    console.log (this.hi);
}

showFullName.call(person); // Output: Hello

// ------------

var mike = {
   checkThis: function() {
       function checkOther(){
           console.log(this);
       }
        checkOther.call(this)
    }
}

mike.checkThis(); // Output: mike Object

// ------------

function a(b,c,d){
    console.log(this);
    console.log(b);
    console.log(c);
    console.log(d);
}

a.call(1,2,3,4); // this = 1

a.apply(1, [2,3,4]); // this = 1
// apply function need to passing in an array of parameters - this only difference with call function.
// So, both methods "a.call(1,2,3,4);" and "a.apply(1, [2,3,4]);" are equivalent with same output.

a(1,2,3,4); // this = window object

// ------------

function sum(){
    var total = 0;
    for (var i = 0; i <arguments.length; i++){
        total += arguments[i];
    }
    return total;
}

var x = sum.call(null, 1,2,3); // Output: 6

var thing = [1,2,3];

var x = sum.apply(null, thing); // Output: 6

// ------------

// 2. Bind

"use strict";
var a = function(){
    console.log(this);
}.bind(2);

a(); // Output: undefined

// Inside bind fucntion, we actually defining "this" keyword paraemter
"use strict";
var a = function(){
    console.log(this);
}.bind(2);

a(); // Output: 2

// Just another way of binding
"use strict";
function a(){
    console.log(this);
};

var f = a.bind(2);
f(); // Output: 2

var mike = {
   checkThis: function() {
       var checkOther = function(){
           console.log(this);
       }.bind(this);
       checkOther();
    }
}

mike.checkThis(); // Output: Object{} - // name of the Object is checkThis as expected
```

## 8. Object creation patterns (Part 1)

```js
// 1. Init method

var Person = {
    init: function(firstName, lastName){
        this.firstName = firstName;
        this.lastName = lastName;
        return this;
    },
    full_name: function(firstName, lastName){
        return this.firstName + " " + this.lastName;
    }
}

var mike = Object.create(Person);
mike.init("Mike", "Penzin");

console.log(mike.full_name()); // Output: Mike Penzin  

// ------------

// 2. Object creation method

var Person = {
    full_name: function(firstName, lastName){
        return this.firstName + " " + this.lastName;
    }
}

var luc = Object.create(Person, {
    firstName: {
        value: "Luc"
    },
    lastName: {
        value: "Besson"
    }
});

var mike = Object.create(Person, {
    firstName: {
        value: "Mike"
    },
    lastName: {
        value: "Penzin"
    }
});

console.log(luc.full_name()); // Output: Luc Besson
console.log(mike.full_name()); // Output: Mike Penzin

// ------------

// 3. Creation function method
var Person = {
    full_name: function(firstName, lastName){
        return this.firstName + " " + this.lastName;
    }
}

function PersonFactory(firstName, lastName){
    var person = Object.create(Person);
    person.firstName = firstName;
    person.lastName = lastName;
    return person;
}

var luc = PersonFactory("Luc", "Besson");

var mike = PersonFactory("Mike", "Penzin");

console.log(luc.full_name()); // Output: Luc Besson
console.log(mike.full_name()); // Output: Mike Penzin

```

## 9. Object creation patterns (Part 2)

```js
// 1. Factory Pattern

var peopleFactory = function(name, age, state){
    var tmp = [];
    tmp.name = name;
    tmp.age = age;
    tmp.state = state;
    tmp.printPerson = function(){
        console.log(this.name + ", " + this.age + ", " + this.state);
    };
    return tmp;
};

var mike = peopleFactory("Mike", 25, "CA");
var john = peopleFactory("John", 34, "SC");

mike.printPerson(); // Output: Mike, 25, CA
john.printPerson(); // Output: john, 34, SC  

// ------------

// 2. Constructor Pattern

var peopleFactory = function(name, age, state){
    this.name = name;
    this.age = age;
    this.state = state;
    this.printPerson = function(){
        console.log(this.name + ", " + this.age + ", " + this.state);
    };
};

var mike = new peopleFactory("Mike", 25, "CA");
var john = new peopleFactory("John", 34, "SC");

mike.printPerson(); // Output: Mike, 25, CA
john.printPerson(); // Output: john, 34, SC  

// In order to test whether an object has in its prototype chain the prototype property of a constructor.

console.log(mike instanceof peopleFactory); // Output: true

// ------------

// 3. Prototype Pattern

var peopleProto = function(){

};

peopleProto.prototype.name = "no name";
peopleProto.prototype.age = 0;
peopleProto.prototype.state = "no state";
peopleProto.prototype.printPerson = function(){
   console.log(this.name + ", " + this.age + ", " + this.state);
};

var mike = new peopleProto();
mike.name = "Mike";
mike.age = 25;
mike.state = "CA";

var john = new peopleProto();
john.name = "John";
john.age = 34;
john.state = "SC";

var defaults = new peopleProto();

mike.printPerson(); // Output: Mike, 25, CA
john.printPerson(); // Output: john, 34, SC  
defaults.printPerson(); // Output: no name, 0, no state

console.log("name" in mike); 
// Output will always be true, 
// since even if name property value not set for object, 
// prototype of the object have default value.

console.log(mike.hasOwnProperty('name')); 
// Out will be true only if property value was set 
// inside this Object (and not prototype defalts). 

// ------------

// 4. Dynamic Prototype Pattern

var peopleDynamicProto = function(name, age, state){
    this.age = age;
    this.name = name;
    this.state = state;

    if( typeof this.printPerson !== 'function') {
        peopleDynamicProto.prototype.printPerson = function(){
           console.log(this.name + ", " + this.age + ", " + this.state);
        };
    }    
};

var mike = new peopleDynamicProto("Mike", 25, "CA");
var john = new peopleDynamicProto("John", 34, "SC");

mike.printPerson(); // Output: Mike, 25, CA
john.printPerson(); // Output: john, 34, SC  

```
## 10. The Singleton Pattern
The Singleton pattern is thus known because it restricts instantiation of a class to a single object. Classically, the Singleton pattern can be implemented by creating a class with a method that creates a new instance of the class if one doesn't exist. In the event of an instance already existing, it simply returns a reference to that object.

Singletons differ from static classes (or objects) as we can delay their initialization, generally because they require some information that may not be available during initialization time. They don't provide a way for code that is unaware of a previous reference to them to easily retrieve them. This is because it is neither the object or "class" that's returned by a Singleton, it's a structure. Think of how closured variables aren't actually closures - the function scope that provides the closure is the closure.

In JavaScript, Singletons serve as a shared resource namespace which isolate implementation code from the global namespace so as to provide a single point of access for functions.

```js
// The simplest singleton implementation in JavaScript is:

var Singleton = {};

// ------------

// Another Implementation

var MySingleton = (function () {

  var INSTANCE;

  function MySingleton(foo) {
    if (!(this instanceof MySingleton)) {
      return new MySingleton(foo);
    }
    this.foo = foo;
  }
  MySingleton.prototype.bar = function () {
    //do something;
  };

  return {
    init: function () {
      if (!INSTANCE) {
        return INSTANCE = MySingleton.apply(null, arguments);
      }
      return INSTANCE;
    },
    getInstance: function () {
      if (!INSTANCE) {
        return this.init.apply(this, arguments);
      }
      return INSTANCE;
    }
  };

}());

var ex1 = MySingleton.getInstance("hi");
var ex2 = MySingleton.getInstance("bye");

console.log(ex1 === ex2); // Output: true
console.log(ex1); // Output: MySingleton {foo: "hi"}
console.log(ex2); // Output: MySingleton {foo: "hi"}

// In this example we use the module pattern once again, 
// in order to enclose the singleton implementation into 
// a lexical closure and provide a public interface for getting its instance.
```
## 11. Promises Patterns
This is a basic pattern for promises.

We can use a promise library for JavaScript http://documentup.com/kriskowal/q/

```js
// Standard callback pattern:

coolAjaxRequest('GET', 'http://myservice.com/dostuff', function(error, result) {
  if(error) {
    // do things with the error here
  } else {
    // do things with the result here
  }
})

// ------------

// Promise pattern:
fancyAjaxRequest('GET', 'http://myservice.com/dostuff')
  .then(function(result) {
    // do things with the result here
  })
  .fail(function(error) {
     // do things with the error here
  })
```

## Useful Links

- [JS the Right Way](http://jstherightway.org/) - This is a guide intended to introduce new developers to JavaScript and help experienced developers learn more about its best practices.
- [How to Learn JavaScript Properly - JavaScript.isSexy](http://javascriptissexy.com/how-to-learn-javascript-properly) - This study guide, which I also refer to as a course outline and a road map, gives you a structured and instructive outline for learning JavaScript properly. 
- [JavaScript // MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript) - Mozilla Developer Network

## Books

- [Eloquent JavaScript](http://eloquentjavascript.net/) - This is a book about JavaScript, programming, and the wonders of the digital. You can read it online.
- [Front-End Developer Handbook 2017](https://www.gitbook.com/book/frontendmasters/front-end-handbook-2017/details) - This is a guide that anyone could use to learn about the practice of front-end development. It broadly outlines and discusses the practice of front-end engineering: how to learn it and what tools are used when practicing it in 2017. The content of the handbook favors web technologies (HTML, CSS, DOM, and JavaScript) and those solutions that are directly built on top of these open technologies. The materials referenced and discussed in the book are either best in class or the current offering to a problem.
- [Craft Academy Bootcamp](https://www.gitbook.com/book/craftacademy/coding-as-a-craft/details) - Craft Academy is a 12-week intensive, practice-oriented course for aspiring junior developers. The course is delivered as a coding bootcamp by Craft Academy in Gothenburg, Sweden. It gives you the basics you need to create, develop and launch web-based applications.
- [Coding as a Craft Bootcamp prep](https://www.gitbook.com/book/craftacademy/caa_precourse/details) - A prep course for junior web developers.
- [Frontend precommit rules for Javascript, SASS](https://www.gitbook.com/book/schibsted-engineers/frontend-pre-commit-rules/details) - The main goal of this set of rules is to establish healthy boundaries where cleaner code will be easier to share, more scalable, more readable and easier to maintain for everyone.
- [Learning JavaScript Design Patterns](https://addyosmani.com/resources/essentialjsdesignpatterns/book/) - Learning JavaScript Design Patterns book by Addy Osmani.
- [JSBooks](http://jsbooks.revolunet.com) - The best free JavaScript resources (books).
- [A book on EcmaScript](https://www.gitbook.com/book/iamanubhavsaini/ecmascript/details) - This is the book you want to read up on JavaScript.
- [Javascript Promises](https://www.gitbook.com/book/samypesse/js-promises/details) - In this book, you'll learn how to use promises in Javascript, and why you should use it.
- [Writing Embedded JavaScript and CSS](https://www.gitbook.com/book/eager/embed/details) - This is a book about how to craft code designed to be embedded into a website. The thing you need to embed might be an analytics tracking code, a UI element like a calendar or form, or a powerful library like Offline.
- [You Don't Know JS (book series)](https://www.gitbook.com/book/asfara/you-dont-know-js/details) - This is a series of books diving deep into the core mechanisms of the JavaScript language. The first edition of the series is now complete.
- [Front-End-Developer - Level 1](https://www.gitbook.com/book/opteamize/front-end-developer/details) - This is the 1st level of the Job Guarantee Front end Developer course from Opteamize, an IBM Coding School. Level 1 includes HTML CSS/basics, Javascript basics & JQuery. Check Opteamize.in for registrations & more info.
- [Front-End-Developer - Level 2](https://www.gitbook.com/book/opteamize/front-end-developer-level-2-/details) - This is the second level of the Job Guarantee Front end Developer course from Opteamize, an IBM Coding School. Level 2 includes CSS, Javascript, Sass, Angularjs, & Placement test. Check opteamize.in for more.
- [Build our own React.js](https://www.gitbook.com/book/swennemans/building-your-own-react-js/details) - In this book/guide we build our own simplified version of React.js. We keep it simple but extensive enough to learn a lot of cool things about React.js and React.js-like libraries.
- [Advanced Functional JavaScript](https://www.gitbook.com/book/rajasharan/functional-javascript/details) - Collection of code snippets to showcase functional aspects of JavaScript.
- [Frontendium Front-end Web Development](https://www.gitbook.com/book/hackpacific/frontendium-front-end-sprint/details) - In 10 weeks, you will learn HTML, CSS, Bootstrap, JavaScript, jQuery, Git and build multiple front-end projects.
- [TypeScript Handbook](https://www.gitbook.com/book/michelc/typescript-handbook/details) - Microsoft TypeScript-Handbook as PDF.
- [Data Structure in JavaScript with ES6/ES2016](https://www.gitbook.com/book/pmary/data-structure-in-javascript/details) - Learn what are the data structures, when to use them, how to implement them and discover the best practices associated. This book also include an overview of the benefits of using the last ES2016 features.







