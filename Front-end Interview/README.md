
[TOC]

[TOC]

# JavaScript

##	forEach() VS map() VS (for..in) VS (for...of)
1.	Both they will  call a provided function on each element in given array. However, the forEach() method doesn’t return anything (can not use break, continue), the map() method will return a new Array of  the same size.
2.	forEach() can be used by map, set and array, map just be used by array
3. for...in is used to iterate object, not good for iterate array, which may iterate over user-defined properties in addition to the array elements
4. The for...of statement creates a loop Iterating over iterable objects (including Array, Map, Set, arguments object and so on)
The following example shows the difference between a for...of loop and a for...in loop. While for...in iterates over property names, for...of iterates over property values:

```JavaScript
// an example
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
​```JavaScript
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
  ​    ```JavaScript
  ​    var b = new Boolean(false);
  ​    if (b) // this condition evaluates to true
  ​    if (b == true) // this condition evaluates to false
  ​    ```
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
# HTML
## HTML Semantic
Semantic HTML is HTML that introduces meaning to the web page rather than just presentation. For example, a <p> tag indicates that the enclosed text is a paragraph. This is both semantic and presentational, because people know what paragraphs are and browsers know how to display them. In HTML4, tags like < b > and < i > are not semantic, because they define only how the text should look (bold or italic) and do not provide any additional meaning.
Examples of semantic HTML tags include the header tags '< h1 > through < h6 >, < blockquote >, < code > and < em >'. There are many more semantic HTML tags.

### Why Semantic HTML is Important
1. semantic code aids accessibility. Specially, many people whose eyes are not good rely on speech browsers to read pages to them. These programs cannot interpret pages very well unless they are clearly explained.
2. Help Search engines to better understand pages.  Search engine need to understand what your content is about when rank you properly on search engines. Semantic code tends to improve your placement on search engines, as it is easier for the "search engine spiders" to understand.
3. It’s easier to read and edit, which saves time and money during maintenance.

## What is Iframe?
* An IFrame (Inline Frame) is an HTML document embedded inside another HTML document on a website.
* The IFrame HTML element is often used to insert content from another source, such as an advertisement, into a Web page.
<iframe src="http://www.w3schools.com">不支持 iframe 的浏览器</iframe>


## Meta tag
* The tag provides metadata about the HTML document. Metadata will not be displayed on the page, but will be machine parsable.
* Meta elements are typically used to specify page description, keywords, author of the document, last modified, and other metadata.
* The metadata can be used by browsers (how to display content or reload page), search engines (keywords), or other web services.

# HTML DOM
## DOM structure
[more details](https://caomingkai.github.io/2018/10/15/Common-DOM-Manipulations/)
> difference between HTMLCollection & NodeList
  * HTMLCollection: a collection of elements
  * NodeList: a collection of all types of nodes: element node/ text node/ comment node
  * convert them to array, to extract info: Array.prototype.slice.call(NodeList)
  * everything in an HTML document is a node:


> navigate across the DOM tree using attributes: [element node, text node, comment node]
  * parentNode---parentElement
  * childNodes---children
  * firstChild---firstElementChild
  * lastChild----lastElementChild
  * nextSibling---nextElementSibling
  * previousSibling---previousElementSibling

## window.onload vs document.onload
* window.onload: When EVERYTHING is loaded. DOM is ready and all the contents including images, css, scripts, sub-frames, etc. finished loaded.
* document.onload: once the DOM is loaded, regardless of the css, scripts,…

## classlist of dom node
```javascript
function addClass(selector, className){
   var elm = document.querySelector(selector);
   if (elm){
      elm.classList.add(className);
      //elm.classList.remove(className);
   }
}
```
## innerHTML, innerText， textContent

```javascript
<p id="test">    This element    contains <span>an inner span</span>. </p>
```
* The values of these properties of the "test" paragraph will be:
* innerText: "This element contains an inner span."  : Just the text, trimmed and space-collapsed.
* innerHtml: " This element     contains <span>an inner span</span>. "   All spacing and inner element tags.
* textContent: " This element     contains an inner span. "  Spacing, but no tags.

## Repaint vs Reflow
* reflow: flow of the elements in the page is changed due to change size or position
* repaint: It happens when you change the look of an element without changing the size and shape. This doesn’t cause reflow as geometry of the element didn’t changed. eg, change visibility

## CreateDocumentFragment
* documentFragment a lightweight or minimal part of a DOM or a subtree of a DOM tree.
* It is very helpful for improving performance when you are manipulating a part of DOM for multiple times.

## Tranverse Dom tree
```JavaScript
 // 广度优先遍历
  function bfs(root) {
    let queue = [root];

    while(queue.length) {
      let curNode = queue.shift();
      console.log(curNode);

      if(!curNode.children.length) {
        continue;
      }

      Array.from(curNode.children).map((child) => queue.push(child));

    }
  }

// 深度优先遍历
  function dfs(root){
    let child = root.firstElementChild;

    while(child) {
      console.log(child);
      dfs(child);
      child = child.nextElementSibling;  
    }
  }
```
### DOM API
* addEventListener & removeEventListener
```JavaScript
// Attach an event handler to the document
document.addEventListener("mousemove", myFunction);

// Remove the event handler from the document
document.removeEventListener("mousemove", myFunction);
```
* createAttribute() & setAttributeNode()
```javascript
function myFunction() {
    var h1 = document.getElementsByTagName("H1")[0];
    var att = document.createAttribute("class");
    att.value = "democlass";
    h1.setAttributeNode(att);
}
```
* createElement() & intersetBefore() & appendChild()
* querySelector & querySelectorAll()

# CSS
## CSS preprocessor
CSS preprocessors take code written in the preprocessed language and then convert that code into the same old css. 3 of the more popular css preprocessors are Sass(用过), LESS, and Stylus
### CSS preprocessor Pros and cons:
* Pros:
  1.	Nested syntax
  2.	Ability to define variables
  3.	Ability to define mixins
  4.	Mathematical functions
  5.	Operational functions (such as “lighten” and “darken”)
  6.	Joining of multiple files
* Cons:
  1.	Debugging is harder
    - Due to having a compilation step, the browser is not interpreting the source files, meaning the CSS line numbers are now irrelevant when trying to debug. This makes debugging a lot harder.

  2.	Maintainance

  3.	Compilation time slows down development
    - Compilation times can be painfully slow, even when using the fastest techniques on a cutting edge machine.
  4.	Performance is compromised
    - Source files may be small, but the generated CSS could be huge. And it’s the generated CSS that counts.

## pt, px, em, rem
* pt are absolute length, 1 pt = 1/72 inch
* px are relative length, different resolution is different length
* em is also relative length, which depends its parents length
* rem is also relative length, which depends root length of HTML

### CSS3 to make shape
* use transform(traslate, rotate)
* use border
```css

  #triangle-up {
    width: 0;
    height: 0;
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 100px solid red;
}
```
 [See more details here](http://www.jqhtml.com/8045.html)

## SASS basic concepts
1. Variables: Variables in SASS start with $ sign
2. Nesting: CSS lacks visual hierarchy while working with child selectors. You have to write selectors and their combinations in separate lines. Nesting provides a visual hierarchy as in the HTML and increases the readability.
3. mixins: mixins are used to include a bunch of properties or group declarations together. It allows for the easy reuse of blocks of code. Use include  to
4. Inheritance: extends are useful for sharing a generic definition with selectors rather than copying it in.
5. If/Else Statements and loops
6. import: separating your codes in small pieces is helpful for expressing your declarations and increasing maintainability and control over the codebase.
7. Math operations: can be used for standard arithmetic or unit conversions.

## Box model
* block: by default, the width is 100%
* inline: width is decided by Content
## Position property
* relative: not change the display property of elements
* absolute: if parents of the elements do not set relative or absolute, the element will locate by the body
  - width of block elements becomes auto, the width of its child element will affect by its width
  - inline elements' display will become blocks
* using relative and absolute, the elements will cover other elements; but we can set z-index as -1
## float
* The float CSS property specifies that an element should be placed along the left or right side of its container, allowing text and inline elements to wrap around it. The element is removed from the normal flow of the web page, but the element will not cover the content of next elements(only cover the box).
* after setting a float property, the element will become a block

[a good article to understand float and position properity](http://www.cnblogs.com/coffeedeveloper/p/3145790.html)
## Clear float
If children set float, the parent will lose height from children. In order to let the parent looks like contain children, we have several method:
1. add new tag in the parent element: < br style="clear:both" />
2. Float (Nearly) Everything
3. set the parent container overflow: hidden,  or overflow: auto;
4. use clearfix/pseudo class:
```javascript
        .clearfix:after {
          content: " ";
          display: block;
          clear: both;
          height: 0;
        }
        .clearfix {
          zoom: 1;
        }
        <div class="clearfix">
        <div class="floated"></div>
        </div>
```
## 5 ways to hidden Elements
1. display: screen readers won’t read the element’s content either. It is as if the element does not exist.
2. visibility:
    - Just like the opacity property, the hidden element will still affect the layout of our web page.
    - The only difference is that this time it will not capture any user interaction when hidden from the user.
    - Additionally, the element will also be hidden from screen readers.
3. opacity:
    - set an element’s transparency;
    - only hides the element visually. The element still occupies its position and affects the layout of the web page.
    - It will also respond to user interaction as well.
    - the element and all its content will be read by screen readers
4. position:  
    - Suppose you have an element that you would like to interact with but you do not want it to affect the layout of your web page.
    - move the element out of the viewport
5. clip-path:

[from here](https://www.sitepoint.com/five-ways-to-hide-elements-in-css/)

## Flexbox layout
### container:
* float, clear, vertical-align for the items inside flexbox will become invalid
* display: inline-flex vs display: flex:----only apply to flex container, to make it display as inline or block won’t affect flex items
  inside
* prosperities:
  1. flex-direction: row | row-reverse | column | column-reverse
  2. flex-wrap: break new line or not when exceeding it container  
        nowrap | wrap | wrap-reverse;
  3. flex-flow: combination of the first two
     ​     <flex-direction> || <flex-wrap>;
  4. align-items: where flex items sit on the cross axis
        flex-start | flex-end | center | baseline | stretch;
  5. justify-content: where the flex items sit on the main axis
        flex-start | flex-end | center | space-between | space-around
### flex items:
* flex: 1 1 20px: three attributes: flex-grow flex-shrink flex-basis
* order: 3: like the smaller will be put in front
* align-self: override its container’s align-items layout, update position of itself
## box-sizing properity
* box-sizing: content-box;
  - The width and height properties include the content, but does not include the padding, border, or margin.
* box-sizing: border-box;
  - The width and height properties include the content, padding, and border, but do not include the margin
## inline element
* padding-top, padding-bottom, margin-top, margin-bottom are invalid for inline elements
* padding-left, padding-right, margin-left, margin-bottom are valid for inline elements
* padding-top, padding-bottom are effective literally, but they did not affect other elements
## CSS Specificity Scoring
* inline style > inner style > external style
* score distribution:
  - HTML tag Element - One
  - Class - Ten
  - ID - Hundred
  - Inline Styles - Thousand
* !important is the biggest

# React
## Why use react framework?
* React is a library for building composable user interfaces. not MVC
* React are based on Components
* reconcilation:
  - When component is first initialized, the render method is called, generating a lightweight representation of our view.
  - From that representation, a string of markup is produced, and injected into the document.
  - When your data changes, the render method is called again.
  - In order to perform updates as efficiently as possible, react diff the return value from the previous call to render with the new one, and generate a minimal set of changes to be applied to the DOM.
  - The data returned from render is neither a string nor a DOM node — it’s a lightweight description of what the DOM should look like.
## Lifecycle
* Mounting phase:These methods are called in the following order when an instance of a component is being created and inserted into the DOM
  - constructor()
  - getDerivedStateFromProps()
  - render()
  - componentDidMount()
* Updating phase：An update can be caused by changes to props or state. These methods are called in the following order when a component is being re-rendered:
  - getDerivedStateFromProps()
  - shouldComponentUpdate()
  - render(): after either new props or new state
  - componentDidUpdate()
* Unmounting phase：This method is called when a component is being removed from the DOM:
  - componentWillUnmount()
[From here](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

<div style="display: flex; justify-content: center;">
 <img src='https://github.com/Attriumph/Interview-Problem-Summary/blob/master/Front-end%20Interview/images/lifecycle.png' width="70%">
</div>

## React Example
```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

# Redux
## Redux Basic
* There are two aspects that React does not solve well, one is code structure and other is communication between components. Therefore, we have Redux(before it, is Flux).
* The key point of Redux is the web application is state machine. A view corresponds to a state.
* All data are stored in one object(store);
* The key concepts are store, state, action and reducer;
* we use createStore to create a store.
* For a store, we could get state by store.getState() and initiate a action by store.dispatch();
* reducer is used to compute state, which is a function could receive two parameters(state and action)
* normally, we pass reducer into createStore()--createStore(reducer) so that reducer will automatically compute and return new state when dispatch a action;
* once state changes, we should automatically update view. This is finished by store.subscribe()
* for large application, we split reducer into different smaller reducers, but we use combineReducers() to combine them

## Keys for Redux usage
* Redux divides components into two types, one is presentational component, the other is container components
* presentational components are responsible for UI, no states; all data are from props;
* container components are responsible for dealing with data and logics, have state
* In redux, we just provide presentational components, redux will create container components automatically
* How we let redux create the container component for our presentational compoents? —— connect()(UI component)
* The rest we need to do is: 1. tell how "state" pass into UI components(becomes props) 2. how let interactions or operation of users become action objects, dispatch to store;
* So, we need mapStateToProps and mapDispatchToProps

```JavaScript
function mapStateToProps(state) {
  return {
    findsState: state
  }
}

function mapDispatchToProps(dispatch) {
  return {
    findsActions: bindActionCreators(findsActions, dispatch)
    // bindActionCreators() call dispath by using findsActions
  }
}

export default connect(mapStateToProps, mapDispatchToProps)(FindsView)
```

## Redux-sagas
* Saga is a middleware to manage the asynchronous operations, which is implemented by generator functions
* Saga could subscribe actions, and then decide what to do next, such as initiate a Asynchronous operation, or initiate another action
* In order to run our Saga, we need to:
  1. create a Saga middleware with a list of Sagas to run
  2. connect the Saga middleware to the Redux store
* all tasks in saga are taken over by Effects, so we can see effects as task units
* There are several factory functions to create effects, such as call(), put(), take()--waiting for a specific action, fork()
* also we have takeEvery() and takeLatest() to execute tasks when we have specific Actions

<img src='https://github.com/Attriumph/Interview-Problem-Summary/blob/master/Front-end%20Interview/images/redux-saga.jpg' width="60%">

# Http

## Features of Http
1. connectionless
2. data type independent
3. stateless

## Post VS Get
1. GET requests include all request data in the URL and POST requests supply additional data from the client (browser) to the server in the message body.
2. Security: GET is less secure compared to POST because data sent is part of the URL
3. history different: for get method, Parameters remain in browser history because they are part of the URL; post: parameter are not saved in browser history
4. restriction on form data length: post no restriction, get has
5. restriction on form data type: get also can use ASCII characters, post method no restriction

## http methods
* GET: The GET method is used to retrieve information from the given server using a given URI. Requests using GET should only retrieve data and should have no other effect on the data.
* HEAD: Same as GET, but transfers the status line and header section only.
* POST: A POST request is used to send data to the server, for example, customer information, file upload, etc. using HTML forms.
*	PUT: Replaces all current representations of the target resource with the uploaded content.
*	DELETE: Removes all current representations of the target resource given by a URI.
*	CONNECT: Establishes a tunnel to the server identified by a given URI.
* OPTIONS: Describes the communication options for the target resource.
*	TRACE: Performs a message loop-back test along the path to the target resource.

# Browser

## What is CORS?

Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers to tell a browser to let a web application running at one origin (domain) have permission to access selected resources from a server at a different origin.

## How to cross origin?
[more details](https://segmentfault.com/a/1190000011145364)
since the same-origin-policy, we cannot send a request to get data from different origin
1. CORS mechanism: it is decided by server of the requested source(the server decides Access-Control-Allow-Origin)
2. JSONP
3. proxy server- nginx
4. websocket(HTML5)
5. nodejs as middleware

## Event delegation:
* define: add a event listener to a single common parent rather than each child, based on the event bubbling mechanism
* when to use?
   we want some code to run when you click on any one of the child elements, we can set the event listener on their parent and have the effect of the event listener bubble to each child, rather than having to set the event listener on every child individually.
[more details here](https://www.cnblogs.com/bfgis/p/5460191.html)

## Event flow
1. event  flow  includes capture phase, target phase and bubble phase.
2.	Capturing phase – the event goes down to the element.
3.	Target phase – the event reached the target element.
4.	Bubbling phase – the event bubbles up from the element
5.  capture and bubble phase are event propagation
6. we can use stopPropogation to stop
## Critical Rending Path
1. Constructing the DOM Tree
2. Constructing the CSSOM Tree
3. Running JavaScript  - parser blocking resource
4. Creating the Render Tree
5. Generating the Layout
6. Painting
## Frame
* FPS: frame per second, for current browser, it's 60 fps
* so, every frame takes 1000/60 = 16.667ms
* the higher, the better user feel

# General Web question
## Responsive Website
1. ```<meta name="viewport" content="width=device-width, initial-scale=1.0">```
2. add media query at css
## SSR VS CSR
* We are using server side rendering for two reasons:
  - performance benefit for our customers
  - Consistent SEO performance
* The main difference is that for SSR your server’s response to the browser is the HTML of your page that is ready to be rendered, while for CSR the browser gets a pretty empty document with links to your javascript. That means for SSR your browser will start rendering the HTML from your server without having to wait for all the JavaScript to be downloaded and executed.
* for SSR, the user can start viewing the page while all of that is happening. For the CSR world, you need to wait for all of the above to happen and then have the virtual dom moved to the browser dom for the page to be viewable.

[From here](https://medium.com/walmartlabs/the-benefits-of-server-side-rendering-over-client-side-rendering-5d07ff2cefe8)
## ansyn vs defer
fetch and executation
* the async attribute is used to indicate to the browser that the script file can be executed asynchronously. The HTML parser does not need to pause at the point it reaches the script tag to fetch and execute, the execution can happen whenever the script becomes ready after being fetched in parallel with the document parsing.
* The defer attribute tells the browser to only execute the script file once the HTML document has been fully parsed.
[From here](https://bitsofco.de/async-vs-defer/)
## Ways to improve website performance
* Minimize HTTP Requests

  Sites are mainly slow because of too many (or too large) HTTP requests. We can eliminate unnecessary request;
  1. combined files: js to a file, css to a file
  2. CSS sprites: CSS Sprites are the preferred method for reducing the number of image requests. Combine your background images into a single image and use the CSS background-image and background-position properties to display the desired image segment.
* Use a Content Delivery Network

  A CDN is essentially many optimized servers around the world that deliver web content to users based on their geographic location. This means big performance improvements for site users. Because, say, if a person accessing your site in India, they will be retrieving web content from a server nearby
* Optimize Images:

  image sizes make a huge difference to site speed. The larger content/images, the slower the site. we could:
   1.	Changing the resolution: reducing the “quality” of the image (and thereby the file size)
   2.	Compressing the picture: increasing the efficiency of image data storage
   3.	Cropping the picture: when cropping, you are cutting out unneeded areas and thus making the image smaller in size
* Put Scripts at the Bottom:

  Javascript files can load after the rest of your page. The simplest solution is to place your external Javascript files at the bottom of your page, just before the close of your body tag. Now more of your site can load before your scripts. Another method that allows even more control is to use the defer or async attributes when placing external .js files on your site.
  1. Async tags load the scripts while the rest of the page loads, but this means scripts can be loaded out of order. Basically, lighter files load first. This might be fine for some scripts, but can be disastrous for others.
  2. The defer attribute loads your scripts after your content has finished loading. It also runs the scripts in order. Just make sure your scripts run so late without breaking your site.
* Add an Expires or a Cache-Control Header

  Web page designs are getting richer and richer, which means more scripts, stylesheets, images, and Flash in the page. A first-time visitor to your page may have to make several HTTP requests, but by using the Expires header you make those components cacheable. This avoids unnecessary HTTP requests on subsequent page views. Expires headers are most often used with images, but they should be used on all components including scripts, stylesheets, and Flash components.
* Gzip Components

  Compression reduces response times by reducing the size of the HTTP response. Gzipping generally reduces the response size by about 70%.
* Put Stylesheets at the Top:

  This is because putting stylesheets in the HEAD allows the page to render progressively.
* Avoid CSS Expressions
* Use GET for AJAX Requests:

  Ajax is that it provides instantaneous feedback to the user because it requests information asynchronously from the backend web server
* Make JavaScript and CSS External:

  Using external files in the real world generally produces faster pages because the JavaScript and CSS files are cached by the browser. JavaScript and CSS that are inlined in HTML documents get downloaded every time the HTML document is requested. This reduces the number of HTTP requests that are needed, but increases the size of the HTML document. On the other hand, if the JavaScript and CSS are in external files cached by the browser, the size of the HTML document is reduced without increasing the number of HTTP requests.
* Use get to ajax request:

   POST is implemented in the browsers as a two-step process: sending the headers first, then sending data. So it's best to use GET, which only takes one TCP packet to send (unless you have a lot of cookies).
* No 404s:

   HTTP requests are expensive so making an HTTP request and getting a useless response (i.e. 404 Not Found) is totally unnecessary and will slow down the user experience without any benefit.
* Reduce Cookie Size:

  HTTP cookies are used for a variety of reasons such as authentication and personalization. Information about cookies is exchanged in the HTTP headers between web servers and browsers. It's important to keep the size of cookies as low as possible to minimize the impact on the user's response time.
* Reduce DNS Lookups
* Minify JavaScript and CSS
* Avoid Redirects
* Remove Duplicate Scripts
* Configure Etags
* Make Ajax Cacheable
* Post-load Components
* Preload Components
* Reduce the Number of DOM Elements
* Minimize the Number of iframes
* Minimize DOM Access
* Optimize CSS Sprites
* Don't Scale Images in HTML
* Make favicon.ico Small and Cacheable
* Avoid Empty Image src


## Cookie
* A cookie is small piece of information stored on local computer by a website you visit.
* Every time the user loads the website, the browser sends the cookie back to the server to notify the website of the user’s previous activity.
* Cookies have a certain life span defined by their creators.
* Cookies allows the site to present user with information customized to fit their needs.
* mainly used for these three purposes:
 1. Session management (user logins, shopping carts)
 2. Personalization (user preferences)
 3.	Tracking (analyzing user behavior)

## Cache
* A web cache (or HTTP cache) is an information technology for the temporary storage (caching) of web documents, such as HTML pages and images, to reduce bandwidth usage, server load, and perceived lag.

## Session
* A session is a server-side storage of information that is used to store the user's interaction with the web site or web application.
* The web application pairs this session id with it's internal database and retrieves the stored variables for use by the requested page.
* It is stored unlimited amount of data.

## Difference between Cache and Cookies
Although cookies and cache are two ways to store data on client’s machine, but there are difference between cache and cookies and they serve different purposes.
1. Cookie is used to store information to track different characteristics related to user, while cache is used to make the loading of web pages faster.
2. Cookies stores information such as user preferences, while cache will keep resource files such as audio, video or flash files.
3. Typically, cookies expire after some time, but cache is kept in the client’s machine until they are removed manually by the user.

## what happends when we type a URL on browser?
1. if requested object is in the browser cache and is fresh, then the browser will display the content.
2. DNS lookup to find the ip address of the server
   check browser cache-> check os cache-> check router cache -> Internet service provider cache(its DNS
     will recursive search)
3. Browser initiate a TCP connection with the server
4. Browser sends a Http request to the server
5. Server handles the incoming request and send response
6. Browser receive the HTTP response;
7. Browser display the html content
   It also will send http request for get image or sth
8. client interaction with server

[From here](http://edusagar.com/articles/view/70/What-happens-when-you-type-a-URL-in-browser)

## Website accessibility consideration:
[From here](https://www.w3.org/WAI/intro/accessibility.php)
### define：
Web accessibility means that developing the website which is accessible to people with disabilities, and that provides a better user experience for everyone.

### specific method
To solve this issue we can use WAI-ARIA (Web Accessibility Initiative – Accessible Rich Internet Applications) to add special ARIA attributes to extend the semantics of the component markup.

[From here](https://webaccess.berkeley.edu/resources/tips/web-accessibility)

1. Choose a content management system that supports accessibility.
2. Use headings correctly to organize the structure of your content.
   - Screen reader users can use heading structure to navigate content. By using headings (< h1 >, < h2>, etc.) correctly and strategically, the content of your website will be well-organized and easily interpreted by screen readers.
3. Include proper alt text for images.
  - Alt text should be provided for images, so that screen reader users can understand the message conveyed by the use of images on the page.
   (This is especially important for informative images (such as infographics). When creating the alt text, the text should contain the message you wish to convey through that image,)
4. Give your links unique and descriptive names.
   - When including links in your content, use text that properly describes where the link will go. Using "click here" is not considered descriptive,
5. Ensure that all content can be accessed with the keyboard alone in a logical way.
   - Users with mobility disabilities may not be able to use a mouse or trackpad. These people are able to access content through the use of a keyboard by pressing the "tab" or "arrow" keys.
6. Design your forms for accessibility.
  - When form fields are not labeled appropriately, the screen reader user does not have the same cues available as the sighted user. It may be impossible to tell what type of content should be entered into a form field.
7. Use tables for tabular data, not for layout
8. Ensure that all content can be accessed with the keyboard alone in a logical way
9. Use ARIA roles and landmarks (but only when necessary)
10. Make dynamic content accessible

# Webpack VS Gulp
* webpack is module bunlder, whose inputs are modules with dependencies, output is static assets, which helps us deploy on the production environment
* gulp is just a task runner, a flow or steam control tool. gulp.task(), gulp.run(), gulp.wathc(),gulp.src(), gulp.dest()
