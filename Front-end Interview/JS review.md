# JavaScript

##	forEach() VS map()
1.	Both they will  call a provided function on each element in given array. However, the forEach() method doesn’t return anything (undefined), the map() method will return a new Array of  the same size.
2.	forEach() can be used by map, set and array, map just be used by array

## What is a Closure?

* A closure is an inner function that has access to the outer function’s variables.
* Why use it?
   1. A closure lets us associate some data (the environment) with a function that operates on that data.
   2. for object data privacy, This has obvious parallels to object oriented programming, where objects allow us to associate some data (the object's properties) with one or more methods.
* sample code:
```JavaScript
function lazy_sum(arr) {
    var sum = function () {
        return arr.reduce(function (x, y) {
            return x + y;
        });
    }
    return sum;
}
var f = lazy_sum([1, 2, 3, 4, 5]); // function sum()
f(); // 15
```

## variable hoisting-- just for no strict mode
* A variable declared by ‘var’, can be accessed before its declaration
* Only the declaration hoisted, not the assignment!
* So it is hoisted with a value as ‘undefined’.

## key features of ES6
* block scoping with let keyword
* default parameters
* rest parameters: a prefix of three dots (...).  The rest parameter allows us to represent an indefinite number of arguments as an array.
  ```JavaScript
  function fn(a,b,...args) {
     //...
  }
  ```
* Spread Operator: consists three dots (...). The spread operator allows us to spread out elements of an array or a string.
* Object Literal: The object literal is one of the most popular patterns for creating objects in JavaScript because of its simplicity.
  1. computed property name
  2. ES6 allows you to eliminate the duplication when a property of an object is same as the local variable name by including the name without a colon and value.
  ```javascript
    function createMachine(name, status) {
      return {
          name,
          status
      };
  }
  ```
* ES6 introduced a new construct for...of that creates a loop iterating over an iterable object such as an Array, a Map, a Set, or an object that implements the iterator.
* destructing assignment: that allows us to take an object or an array and destructure it into individual variables.
* Template Literals: a template literal uses backticks , it has the following features:
   1. Multiline string: a string that can span multiple lines.
   2. String formatting: the ability to substitute part of the string for the values of a variable or an expression.
   3. HTML escaping: the ability to transform a string so that it is safe to include in HTML.
* ES6 modules: export variables, functions, classes from a module and reuse them in other modules.  
* introduce class and also extends and super key words
    ```JavaScript
    class Animal {
        constructor(type) {
            this.type = type;
          }
          identify() {
            console.log(type);
          }
        }
  ```
* Symbol: ES6 added the Symbol as a new primitive type.
* Promise
* Generator
* Iterator
* Map and Set
* Arrow function: Until arrow functions, every new function defined its own this value (based on how function was called)
  - An arrow function does not have its own this; the this value of the enclosing lexical context is used i.e. Arrow functions follow the normal variable lookup rules. So while searching for this  which is not present in current scope they end up finding this from its enclosing scope .
  - Since arrow functions do not have their own this, the methods call() or apply() can only pass in parameters. thisArg is ignored.
[more details about arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)  
[more details about es6 see here](http://www.javascripttutorial.net/es6/)

## What is Promise?
Since JavaScript is single-thread language, so we need a lot of asynchronous functions. However, sometime we got a bunch of ugly nested code for asynchronous operation. Therefore, we introduce Promise to solve this problem.

* A Promise object serves as a link between the executor(resolve, reject) and the consuming functions, which needs the result or error of executor.resolve and reject are built-in functions in JS
* In executor, we do the asynchronous action. After it is done, we will call the consuming functions.
* When the promise is created, this executor function runs automatically. Since it contains the producing code, that will eventually produce a result(consuming function will use the result)
* The resulting promise object has internal properties: state(pending, fulfilled and rejected) and result

* also, we could use '.then' after a promise, so we can control the sequence of a series of asynchronous action
* also, we have promise.all() and promise.race()
[more details here](https://javascript.info/promise-basics)
## What is generator?
* got bunch of nested code when dealing with many asynchronous functions, better then Promise
* generator can be viewed as a special function in ES6, which allows us to control the process of the function
* generator could pause its own process by yield inside and restart it from outside
* we create a generator object to control its process, the generator object is also a iterator object

## callback
A callback is a function to be executed after another function is executed, which is:
1.	passed as an argument to another function
2.	is invoked after some kind of event
3.  once its parent function completes, the function passed as an argument is then called


## Event loop and message Queue
* JavaScript use event loop and message queue to notify the accomplishment of ayschronous operations
* A JavaScript runtime uses a message queue, which is a list of messages to be processed. Each message has an associated function which gets called in order to handle the message.
* At some point during the event loop, the Js runtime starts handling the messages on the queue, starting with the oldest one. To do so, the message is removed from the queue and its corresponding function is called with the message as an input parameter.
 [More details about event loop, message queue, ansychronous and synchronous](https://segmentfault.com/a/1190000004322358)
## callback vs Promises
* we must know what to do with the result before loadScript is called. Also, There can be only one callback.
* Promises allow us to do things in the natural order. First, we get our promise object, and .then we write what to do with the result.
  also, We can call .then on a Promise as many times as we want.

## fetch() VS AJAX

## apply(), call(), bind()
* Both these functions are used to bind 'this' to functions. JavaScript function has their owner.
* The only difference between apply and call is parameters for them. The call() method takes arguments separately. The apply() method takes arguments as an array.
* bind() will create new function, it will not execute immediately, but call and bind will

## Object VS array
1. array has order, object does not have order
2. when delete or add element in array, typically, it will be more expensive

## Map vs Object
1. Key field: in Object, the keys MUST be simple types — either integer or string or symbols.
   But in Map it can be any data type (an object, an array, etc…).
2. Element order: in Map, original order of elements (pairs) is preserved(so iterable), while in Object, it isn’t.
3. Inheritance: Map is an instance of Object
4. compared with object, map has a lot of convenient method for data operation, such as size(), remove element, forEach

## Array VS set
1. set does not have duplicates, so when we need non-duplicate, we better use set
2. array is better  when we need quick access to element by index and do heavy modification
## The way to judge the data type in js
1. Object.prototype.toString.call(), return [Object，type]
2. jquery.type();


## splice() vs slice()
1. The splice() method adds/removes items to/from an array, and returns the removed item(s).
2. slice() of array work likes subString() of string


## Prototype
 A prototype is an internal object from which other objects inherit properties. Its main purpose is to allow multiple instances of an object to share a common property.

## Class inheritance VS prototype inheritance
> Class Inheritance:
* instances inherit from classes and create sub-class relationships.
* Instances are typically instantiated via constructor functions with the new keyword.  
* ES6 syntax extending classes is much easier to understand.
* There are two new keywords: extends and super.
*  The extends keyword sets up the inheritance relationship between the parent and child classes.
* The super keyword invokes the constructor on the parent class.
> Prototypal Inheritance:
* instances inherit directly from other objects.
* Instances are typically created via factory functions or Object.create().
* Instances may be composed from many different objects, allowing for easy selective inheritance. We all know that JavaScript doesn’t supports multiple inheritance. But there’s a way to “mimic multiple inheritance” in prototype-based languages. But it cannot be done in class-based languages which does not support multiple inheritance.
* before ES6, we use the following code to inherit a object

```javascript
function inherits(Child, Parent) {
    var F = function () {};
    F.prototype = Parent.prototype;
    Child.prototype = new F();
    Child.prototype.constructor = Child;
}

function Student(props) {
    this.name = props.name || 'Unnamed';
}

Student.prototype.hello = function () {
    alert('Hello, ' + this.name + '!');
}

function PrimaryStudent(props) {
    Student.call(this, props);
    this.grade = props.grade || 1;
}

// 实现原型继承链:
inherits(PrimaryStudent, Student);

// 绑定其他方法到PrimaryStudent原型:
PrimaryStudent.prototype.getGrade = function () {
    return this.grade;
};
```
* after ES6, we use the following codes
```JavaScript
class Student {
    constructor(name) {
        this.name = name;
    }

    hello() {
        alert('Hello, ' + this.name + '!');
    }
}

class PrimaryStudent extends Student {
    constructor(name, grade) {
        super(name); // 记得用super调用父类的构造方法!
        this.grade = grade;
    }

    myGrade() {
        alert('I am at grade ' + this.grade);
    }
}

```

##  Debounce & Throttling

* Debounce: For events like keydown, scroll, we don’t want to trigger event in the middle of it, but only want to trigger after user pause! (ie. we only care the final result)
* Throttling: For events like mouseover, we don’t want to trigger event every for every single move, but only want to trigger it every 200ms if such event happens (ie. we only care sample results)

```JavaScript
// Debounce
let textarea = document.querySelector("textarea");
  let timeout;
  textarea.addEventListener("input", () => {
    clearTimeout(timeout);  
    timeout = setTimeout(() => {console.log("Typed!"); }, 500);
  });

// Throttling
  let scheduled = true;
  window.addEventListener("mousemove", event => {
    if (scheduled) {
      document.body.textContent = `Mouse at ${event.pageX}, ${event.pageY}`;
      scheduled = false;
      setTimeout(() => { scheduled = true; }, 1000);
    }
  });

```
[From here](https://caomingkai.github.io/)

## variable hoisting(only under un strict mode)
A variable declared by ‘var’, can be accessed before its declaration
Only the declaration hoisted, not the assignment!
So it is hoisted with a value as ‘undefined’.

## Talk about 'this'
* Since JavaScript does not have real class (everything is object),  so functions do not know who is their owner. When a object call a function, it should tell the function that I am the current owner of you  and you should use my properties to execute. This is what this does.
* The this reference ALWAYS refers to (and holds the value of) an object—a singular object—and it is usually used inside a function or a method
* two special condition is constructor and arrow function
* this in arrow function is lexical scoping
* for constructor, this refers the new object

## CommonJS, AMD, RequireJS, ES6 Modules
All of them are talking about javascript modules.
JavaScript Modules refer to a small units of independent, reusable code. They have distinct functionality, allowing them to be added, removed without disrupting the system.
* CommonJS uses the keywords require and exports. require is a function used to import functions from another module. exports is an object where any function put into it will get exported.(we could use nodeJS implmentation)
* Asynchronous Module Definition (AMD): AMD was born since CommonJS wasn’t suited for the browsers early on. As the name implies, it supports asynchronous module loading.
* RequireJS：implements the AMD API. It loads the plain JavaScript files as well as modules by using plain script tags. It includes an optimizing tool which can be run while deploying our code for better performance.


## How to implement a Queue by using JS?
1.	Two pointers and A object
2.	Use array—reverse();

```javascript
function Queue() {
    this._oldestIndex = 1;
    this._newestIndex = 1;
    this._storage = {};
}

Queue.prototype.size = function() {
    return this._newestIndex - this._oldestIndex;
};

Queue.prototype.enqueue = function(data) {
    this._storage[this._newestIndex] = data;
    this._newestIndex++;
};

Queue.prototype.dequeue = function() {
    var oldestIndex = this._oldestIndex,
        newestIndex = this._newestIndex,
        deletedData;

    if (oldestIndex !== newestIndex) {
        deletedData = this._storage[oldestIndex];
        delete this._storage[oldestIndex];
        this._oldestIndex++;

        return deletedData;
    }
	};
```
## Common Js functions
* Array
  - Array.isArray(arr)
  - arr.join(".")
  - push()/pop()
  - shift()/unshift()
  - reverse()
  - sort()
  - arr.concat(): arr.concat("test1", ["test2"]) return a new arr
  - slice():  return a new Array
  - splice(): modify the original Array
  - indexOf()
  - every() / some()
  - filter()/ map()/ forEach()
  - reduce()
* String
  - charAt()
  - indexOf()
  - match()
  - search()
  - replace(): return a new string
  - split()
  - concat()
  - slice()/substring()
  - trim()
  - escape(string)/unescape(string)
  - encodeURI(string)/decodeURI(string)
  
[From here](http://realtcg.com/2017/05/13/JavaScript%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0%E6%80%BB%E7%BB%93-%E4%B8%80/)
