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

## Callback
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

## HTML DOM
### Tranverse Dom tree
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
  - width of block elements becomes auto
  - inline elements' display will become blocks
* using relative and absolute, the elements will cover other elements; but we can set z-index as -1
## float
* The float CSS property specifies that an element should be placed along the left or right side of its container, allowing text and inline elements to wrap around it. The element is removed from the normal flow of the web page, but the element will not cover the content of next elements(only cover the border).
* after setting a float property, the element will become a block

## Clear float
If children set float, the parent will lose height from children. In order to let the parent looks like contain children, we have several method:
1. add new tag in the parent element: < br style="clear:both" />
2. Float (Nearly) Everything
3. use psedou class after
```html
<div class="l-form-row">
            <div class="l-form-label"></div>
            ....
        </div>
        <style>
            .l-form-row:after {
                clear: both;
                content: "\0020";
                display: block;
                height: 0;
                overflow: hidden
            }
        </style>
```
4. set the parent container overflow: hidden,  or overflow: auto;
5. use clearfix:
```
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

## Event emitter
### When to use it?
* If when a certain event happens, we have to deal many type of manipulation for that event’s result, then it is better to use the event emitter pattern. Instead put all functions inside an event callback, we subscribe all the function to that event, when the event happens, we emit the event!

# React-Redux
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

# General Web question

## responsive Website
* <meta name="viewport" content="width=device-width, initial-scale=1.0">
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
1. if requested object is in the browser cache and is fresh, move on to step 7
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
# AngularJS VS React
* two way binding model VS one way data flow

# Webpack VS Gulp
* webpack is module bunlder, whose inputs are modules with dependencies, output is static assets, which helps us deploy on the production environment
* gulp is just a task runner, a flow or steam control tool. gulp.task(), gulp.run(), gulp.wathc(),gulp.src(), gulp.dest()
