# JavaScript

##	forEach() VS map() VS (for..in) VS (for...of)
1.	Both they will  call a provided function on each element in given array. However, the forEach() method doesn’t return anything (can not use break, continue), the map() method will return a new Array of  the same size.
2.	forEach() can be used by map, set and array, map just be used by array
3. for...in is used to iterate object, not good for iterate array, which may iterate over user-defined properties in addition to the array elements
4. The for...of statement creates a loop Iterating over iterable objects (including Array, Map, Set, arguments object and so on)
The following example shows the difference between a for...of loop and a for...in loop. While for...in iterates over property names, for...of iterates over property values:

```JavaScript

var arr = [3, 5, 7];
arr.foo = 'hello';

for (var i in arr) {
   console.log(i); // logs "0", "1", "2", "foo"
   console.log("length is ",arr.length) //3
}

for (var i of arr) {
   console.log(i); // logs 3, 5, 7
}
```

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

## Hoisting -- just for no strict mode
* A variable declared by ‘var’, can be accessed before its declaration
* Only the declaration hoisted, not the assignment! So it is hoisted with a value as ‘undefined’.
* Function expressions in JavaScript are not hoisted. But, Fucntion declaration could be hoisted
## Key features of ES6
* block scoping with let keyword
* default parameters
* rest parameters: a prefix of three dots (...).  The rest parameter allows us to represent an indefinite number of arguments as an array.we use the rest parameters to collect arguments from the second one to the end. We then multiply them by the first one. This example is using an arrow function, which is introduced in the next section.
```JavaScript
  function multiply(multiplier, ...theArgs) {
    return theArgs.map(x => multiplier * x);
  }

  var arr = multiply(2, 1, 2, 3);
  console.log(arr); // [2, 4, 6]
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
* The await operator is used to wait for a Promise. It can only be used inside an async function
### Promise example
```JavaScript
function loadScript(src) {
  return new Promise(function(resolve, reject) {
    let script = document.createElement('script');
    script.src = src;

    script.onload = () => resolve(script);
    script.onerror = () => reject(new Error("Script load error: " + src));

    document.head.append(script);
  });
}

let promise = loadScript("https://cdnjs.cloudflare.com/ajax/libs/lodash.js/3.2.0/lodash.js");

promise.then(
  script => alert(`${script.src} is loaded!`)  
).catch(
  error => alert(`Error: ${error.message}`));

promise.then(script => alert('One more handler to do something else!'));
```

[more details here](https://javascript.info/promise-basics)

## Callback
A callback is a function to be executed after something happended, which is:
1. passed as an argument to another function
2. is invoked after some kind of event
3. once its parent function completes, the function passed as an argument is then called
4. not only for ansychronous operations
5. Callbacks are a way to make sure certain code doesn’t execute until other code has already finished execution.
6. who call the callback when something happens? --- event loop and message queue mechanism

[a good article to understand callback](https://codeburst.io/javascript-what-the-heck-is-a-callback-aba4da2deced)


## Callback vs Promises
* We must have a ready callback function when calling function(args, callbackFun). Also, There can be only one callback. Therefore,
  we get a nested and badly readable code when we have a series of asynchronous functions
* Promises makes the code more readable, especially when using async and await. First, we get our promise object, and .then we write what to
  do with the result.

[compare callback vs promise with code](https://medium.com/front-end-hacking/callbacks-promises-and-async-await-ad4756e01d90)

## What is generator?
  * got bunch of nested code when dealing with many asynchronous functions, better then Promise
  * generator can be viewed as a special function in ES6, which allows us to control the process of the function
  * generator could pause its own process by yield inside and restart it from outside
  * we create a generator object to control its process, the generator object is also a iterator object

## Observable
  * see the following code
  ```JavaScript
  var observable = Rx.Observable.create(function (observer) {
    observer.next(1);
    observer.next(2);
    observer.next(3);
    setTimeout(() => {
      observer.next(4);
      observer.complete();
    }, 1000);
  });

  console.log('just before subscribe');
  observable.subscribe({
    next: x => console.log('got value ' + x),
    error: err => console.error('something wrong occurred: ' + err),
    complete: () => console.log('done'),
  });
  console.log('just after subscribe');
  ```
  * Which executes as such on the console:

    - just before subscribe
    -  got value 1
    -  got value 2
    -  got value 3
    -  just after subscribe
    -  got value 4
    -  done

  * observable is not just from ayschronous operations  
  * observable is a function, which can be observed by observer
  * observer is a object, which has three callback: next, error, complete
  * how to subscribe the observable?
          observable.subsribe(observer)
  * how to manage the relationships between observable and observer? -- subscription
          var subscription1 = observable.subscribe(observer1);
  * how to unsubscribe?  --- subscription1.unsubscribe();
  * Subscribing to an Observable is analogous to calling a Function.
  *  two Observable subscribes trigger two separate side effects. As opposed to EventEmitters which share the side effects and have eager execution regardless of the existence of subscribers, Observables have no shared execution and are lazy.
  * observable will not automatically run, which is opposed to promise.

  ## Event loop and message Queue
  * JavaScript use event loop and message queue to notify the accomplishment of ayschronous operations
  * single thread means single javaScript engine, but we have other thread, such as ajax thread, runtime
  * A JavaScript runtime uses a message queue, which is a list of messages to be processed. Each message can be views as a callbackFun with response of asynchronous request
  * At some point during the event loop, the Js runtime starts handling the messages on the queue, starting with the oldest one. To do so, the message is removed from the queue and its corresponding function is called with the message as an input parameter.

  [More details about event loop, message queue, ansychronous and synchronous](https://segmentfault.com/a/1190000004322358)

## Comparison between Data structures
### Object VS Array
1. array has order, object does not have order
2. when delete or add element in array, typically, it will be more expensive

### Map vs Object
1. Key field: in Object, the keys MUST be simple types — either integer or string or symbols.
   But in Map it can be any data type (an object, an array, etc…).
2. Element order: in Map, insertion order of elements (pairs) is preserved(so iterable), while in Object, it isn’t.
3. Inheritance: Map is an instance of Object
4. compared with object, map has a lot of convenient method for data operation, such as size(), remove element, forEach

### Array VS Set
1. set does not have duplicates, so when we need non-duplicate, we better use set
2. Checking whether an element exists in a collection using indexOf for arrays is slow.
3. array is better  when we need quick access to element by index and do heavy modification
4. Set objects let you delete elements by their value. With an array you would have to splice based on an element's index.---set.delete('foo');


## Prototype
 A prototype is an internal object from which other objects inherit properties. Its main purpose is to allow multiple instances of an object to share a common property.

## Class inheritance VS prototype inheritance

|Class-based (Java) |	Prototype-based (JavaScript)|
| ------ | ------ |
Class and instance are distinct entities.	| All objects can inherit from another object.
Define a class with a class definition; instantiate a class with constructor methods.	| Define and create a set of objects with constructor functions.
Create a single object with the new operator.	| Same.
Construct an object hierarchy by using class definitions to define subclasses of existing classes. |	Construct an object hierarchy by assigning an object as the prototype associated with a constructor function.
Inherit properties by following the class chain.	| Inherit properties by following the prototype chain.
Class definition specifies all properties of all instances of a class. Cannot add properties dynamically at run time.	| Constructor function or prototype specifies an initial set of properties. Can add or remove properties dynamically to individual objects or to the entire set of objects.

## Inheritance in JavaScript
* Every object has a ```__proto__``` object property (except Object);
* The special property ```__proto__``` is set when an object is constructed; it is set to the value of the constructor's prototype property.
* every function has a prototype object property.
* Because an object has a single associated prototype, JavaScript cannot dynamically inherit from more than one prototype chain.
* In JavaScript, you can have a constructor function call more than one other constructor function within it. This gives the illusion of multiple inheritance.


### 1. based on example of MDN

  <img src='https://github.com/Attriumph/Interview-Problem-Summary/blob/master/Front-end%20Interview/images/hierachy1.png' width="40%">


* Two ways to implement inheritance based on MDN documents
    1. use Object.create(): three steps
    2. use new Father: 1 step, lack change children's constructor?????
  see code below:

```javaScript

function Employee(name, dept) {
  this.name = name || '';
  this.dept = dept || 'general';
}

// the first way to inherit a prototype
function Manager() {
  Employee.call(this);
  this.reports = [];
}
Manager.prototype = Object.create(Employee.prototype);
Manager.prototype.constructor = Manager;

function WorkerBee() {
  Employee.call(this);
  this.projects = [];
}
WorkerBee.prototype = Object.create(Employee.prototype);
WorkerBee.prototype.constructor = WorkerBee;

// anther qucik way to inherit
// but in this case:
// If we want to change the value of an object property at run time and have the new value be inherited by
//all descendants of the object, we cannot define the property in the object's constructor function.
// Instead, we add it to the constructor's associated prototype.

function WorkerBee(projs) {

 this.projects = projs || [];
}
WorkerBee.prototype = new Employee;

function Engineer(mach) {
   this.dept = 'engineering';
   this.machine = mach || '';
}
Engineer.prototype = new WorkerBee;

//have the constructor add more properties by directly calling the constructor function for an object higher in the prototype chain
function Engineer(name, projs, mach) {
  WorkerBee.call(this, name, 'engineering', projs);
  this.machine = mach || '';
}
```
### 2. based on liaoxuefeng
* a universal way to implement inheritance in javaScript before ES6
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

## Talk about 'this'
* Since JavaScript does not have real class (everything is object),  so functions do not know who is their owner. When a object call a function, it should tell the function that I am the current owner of you  and you should use my properties to execute. This is what this does.
* The this reference ALWAYS refers to (and holds the value of) an object—a singular object—and it is usually used inside a function or a method
* two special condition is constructor and arrow function
* this in arrow function is lexical scoping
* for constructor, this refers the new object

## Common Js functions
* Array
  - Array.isArray(arr)
  - arr.join(".")
  - push()/pop()
  - shift()/unshift()
  - reverse()
  - sort()
  - arr.concat(): arr.concat("test1", ["test2"]) returns a new array.
  - slice():  return a new Array
  - splice(): modify the original Array
  - indexOf()
  - every() / some()
  - filter()/ map()/ forEach()
  - reduce(): applies callback(firstValue, secondValue) to reduce the list of items down to a single value and returns that value.
  - find():the value of the first element in the array that satisfies the provided testing function. Otherwise undefined is returned.
* String
  - charAt()
  - indexOf()/lastIndexOf()
  - startsWith()/endsWith(): determines whether a string begins/ends with the characters of a specified string
  - match(): [returns depends on whether regexpress has flag 'g'](https://mzl.la/1pFXfp8)
  - search() : return the index of the first match between the regular expression and the given string
  - replace(): [return a new string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace)
  - split()
  - concat()
  - slice()/substring()
  - trim()
  - encodeURIComponent()/decodeURIComponent()
  - encodeURI(string)/decodeURI(string)  [difference see here](https://www.jianshu.com/p/075f5567c9a1)
* Number Object
  - Number.MAX_VALUE
  - Number.MIN_VALUE
  - Number.isInterger()
  - Number.isNaN()
* Math object
  - Math.PI  (3.14....)
  - Math.abs()
  - Math.sin(), Math.cos(), Math.tan()
  - Math.pow(base, exponent), Max.log10(), Math.log2()
  - Math.floor(), Math.ceil()---returns the smallest integer greater than or equal to a given number.
  - Math.min(), Math.max(), coudld be mor than two values
  - Math.random() --- The Math.random() function returns a floating-point, pseudo-random number in the range 0–1 (inclusive of 0, but not 1)
  - Math.round()--- returns the value of a number rounded to the nearest integer.
  - Math.sqrt(), Math.cbrt()
  - Math.sign() --- return 1, 0, -1 indicating the sign of a number

[From here](http://realtcg.com/2017/05/13/JavaScript%E5%B8%B8%E7%94%A8%E5%87%BD%E6%95%B0%E6%80%BB%E7%BB%93-%E4%B8%80/)
## arguments objects
* it is a array-like object
* Using the arguments object, we can call a function with more arguments than it is formally declared to accept. This is often useful if you don't know in advance how many arguments will be passed to the function.
```JavaScript
function myConcat(separator) {
   var result = ''; // initialize list
   var i;
   // iterate through arguments
   for (i = 1; i < arguments.length; i++) {
      result += arguments[i] + separator;
   }
   return result;
}

// returns "red, orange, blue, "
myConcat(', ', 'red', 'orange', 'blue');

// returns "elephant; giraffe; lion; cheetah; "
myConcat('; ', 'elephant', 'giraffe', 'lion', 'cheetah');
```
[From MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)

## Event emitter
### When to use it?
* If when a certain event happens, we have to deal many type of manipulation for that event’s result, then it is better to use the event emitter pattern. Instead put all functions inside an event callback, we subscribe all the function to that event, when the event happens, we emit the event!

## CommonJS, AMD, RequireJS, ES6 Modules
All of them are talking about javascript modules.
JavaScript Modules refer to a small units of independent, reusable code. They have distinct functionality, allowing them to be added, removed without disrupting the system.
* CommonJS uses the keywords require and exports. require is a function used to import functions from another module. exports is an object where any function put into it will get exported.(we could use nodeJS implmentation)
* Asynchronous Module Definition (AMD): AMD was born since CommonJS wasn’t suited for the browsers early on. As the name implies, it supports asynchronous module loading.
* RequireJS：implements the AMD API. It loads the plain JavaScript files as well as modules by using plain script tags. It includes an optimizing tool which can be run while deploying our code for better performance.


## How to implement a Queue by using JS?
1.	Two pointers and A object
2.	Use array, shift() for dequeue;

```javascript
function Queue() {
    this._oldestIndex = 0;
    this._newestIndex = 0;
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
## Some small but important details for JavaScript
### apply(), call(), bind()
* Both these functions are used to bind 'this' to functions. JavaScript function has their owner.
* The only difference between apply and call is parameters for them. The call() method takes arguments separately. The apply() method takes arguments as an array.
* bind() will create new function, it will not execute immediately, but call and bind will
### The way to judge the data type in js
1. Object.prototype.toString.call(), return [Object，type]
2. jquery.type();
3. typeof operator

      |type|return|
      | ------ | ------ |  
      |Undefined	|"undefined"|
      Null |	"object"
      Boolean	|"boolean"
      Number/NaN |	"number"
      String |	"string"
      Symbol | 	"symbol"
      Function object | (	"function"
      Any other object|	"object"

### falsy values
* The following values evaluate to false (also known as Falsy values):    
  * false
  * undefined
  * null
  * 0
  * NaN
  * the empty string ("")

* All other values, including all objects, evaluate to true when passed to a conditional statement.      
* Do not confuse the primitive boolean values true and false with the true and false values of the Boolean object. For example:
      ```JavaScript
      var b = new Boolean(false);
      if (b) // this condition evaluates to true
      if (b == true) // this condition evaluates to false
      ```
### if (key in object) VS if (object.hasOwnProperty(key))
* the in operator returns true if the specified property is in the specified object or its prototype chain.
* in will also return true if key gets found somewhere in the prototype chain,
* whereas Object.hasOwnProperty (like the name already tells us), will only return true if key is available on that object directly (its "owns" the property).
### !!(expression) in js
* it convert expression into boolean
### Ways to judge if two object are same
*  `_.isEqual(obj1, obj2)` method of lodash.js and underscore.js
[from here](https://stackoverflow.com/questions/13632999/if-key-in-object-or-ifobject-hasownpropertykey)
### undefined and null
* The undefined value behaves as false when used in a boolean context;The undefined value converts to NaN when used in numeric context.
* When you evaluate a null variable, the null value behaves as 0 in numeric contexts and as false in boolean contexts
* variables that are hoisted return a value of undefined. So even if you declare and initialize after you use or refer to this variable, it still returns undefined
### function scope vs block scope
* block scope is delimited by a pair of curly brackets
* function scope is delimited by function
* In web pages, the global object is window

### Data type conversion
* In expressions involving numeric and string values with the **+ operator**, JavaScript converts numeric values to strings
* statements involving other operators, JavaScript does not convert numeric values to strings.
* convert strings to numbers: parseInt() and parseFloat()
### Object Literals
* Object property names can be any string, including the empty string. If the property name would not be a valid JavaScript identifier or number, it must be enclosed in quotes. Property names that are not valid identifiers also cannot be accessed as a dot (.) property, but can be accessed and set with the array-like notation("[]").
* identifier are a sequence of characters
```JavaScript
var foo = {a: 'alpha', 2: 'two'};
console.log(foo.a);    // alpha
console.log(foo[2]);   // two
//console.log(foo.2);  // SyntaxError: missing ) after argument list
//console.log(foo[a]); // ReferenceError: a is not defined
console.log(foo['a']); // alpha
console.log(foo['2']); // two
```

### Arrow function
* does not have its own this, arguments, super
* An arrow function does not have its own this; the this value of the enclosing execution context is used(箭头函数捕捉闭包上下文的this值).
* 在箭头函数出现之前，每一个新函数都重新定义了自己的 this 值

### Arrays are also objects in JavaScript
* JavaScript does not have an explicit array data type,if you supply a non-integer value to the array operator in the code below, a property will be created in the object representing the array, instead of an array element. It actually not array element, does not change array length
* also, we cannot access it by for...of
```JavaScript
var arr = [];
arr[3.4] = 'Oranges';
```
### Three native ways to list/traverse object properties:

* for...in loops
This method traverses all enumerable properties of an object and its prototype chain
* Object.keys(o)
This method returns an array with all the own (not in the prototype chain) enumerable properties' names ("keys") of an object o.
* Object.getOwnPropertyNames(o)

### Using the Object.create method create object
* Objects can also be created using the Object.create() method. This method can be very useful, because it allows you to choose the prototype object for the object you want to create, without having to define a constructor function.
```JavaScript
// Animal properties and method encapsulation
var Animal = {
  type: 'Invertebrates', // Default value of properties
  displayType: function() {  // Method which will display type of Animal
    console.log(this.type);
  }
};

// Create new animal type called animal1
var animal1 = Object.create(Animal);
animal1.displayType(); // Output:Invertebrates

// Create new animal type called Fishes
var fish = Object.create(Animal);
fish.type = 'Fishes';
fish.displayType(); // Output:Fishes
```
### 'this' used in form
When combined with the form property, this can refer to the current object's parent form. In the following example, the form myForm contains a Text object and a button. When the user clicks the button, the value of the Text object is set to the form's name. The button's onclick event handler uses this.form to refer to the parent form, myForm.
```html
<form name="myForm">
<p><label>Form name:<input type="text" name="text1" value="Beluga"></label>
<p><input name="button1" type="button" value="Show Form Name"
     onclick="this.form.text1.value = this.form.name">
</p>
</form>
```
