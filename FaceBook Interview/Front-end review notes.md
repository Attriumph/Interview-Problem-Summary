# JavaScript

##	forEach() VS map()
1.	the forEach() method doesn’t return anything (undefined). It simply calls a provided function on each element in your array. However, the map() method will also call a provided function on every element in the array and returns a new Array of the same size.
2.	forEach can be used by map, set and array, map just be used by array

## What is a Closure?

A closure is an inner function that has access to the outer function’s variables.

## variable hoisting-- just for no strict mode
* A variable declared by ‘var’, can be accessed before its declaration
* Only the declaration hoisted, not the assignment!
* So it is hoisted with a value as ‘undefined’.

## The way to judge the data type in js
Object.prototype.toString.call(), return [Object，type]
jquery.type();

## callback
A callback is a function to be executed after another function is executed, which is:
1.	passed as an argument to another function
2.	is invoked after some kind of event
3.  once its parent function completes, the function passed as an argument is then called

## What is Promise?
Since JavaScript is single-thread language, so we need a lot of asynchronous functions. However, sometime we got a bunch of ugly nested code for asynchronous operation. Therefore, we introduce Promise to solve this problem.

* A Promise object serves as a link between the executor(resolve, reject) and the consuming functions, which will receive the result or error.
* In executor, we do the asynchronous action. After it is done, we will call the consuming functions.
* When the promise is created, this executor function runs automatically. Since it contains the producing code, that will eventually produce a result(consuming function will use the result)
* The resulting promise object has internal properties: state(pending, fulfilled and rejected) and result

* also, we could use '.then' after a promise, so we can control the sequence of a series of asynchronous action
* also, we have promise.all() and promise.race()

## What is generator?
* got bunch of nested code when dealing with many asynchronous functions, better then Promise
* generator can be viewed as a special function in ES6, which allows us to control the process of the function
* generator could pause its own process by yield inside and restart it from outside
* we create a generator object to control its process, the generator object is also a iterator object

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

## splice vs slice
1. The splice() method adds/removes items to/from an array, and returns the removed item(s).
2. slice() of array work likes subString() of string

## Key concepts of Redux
* There are two aspects that React does not solve well, one is code structure and other is comunication of component. Therefore, we have Redux(before it, is Flux).
* The key point of Redux is the web application is state machine. A view corresponds to a state.
* All data are stored in one object(store);
* The key concepts are store, state, action and reducer;
* we use createStore to create a store.
* For a store, we could get state by store.getState() and initiate a action by store.dispatch();
* reducer is used to compute state, which is a function could receive two parameters(state and action)
* normally, we pass reducer into createStore()--createStore(reducer) so that reducer will automatically compute and return new state when dispatch a action;
* once state changes, we should automatically update view. This is finished by store.subscribe()
* for large application, we split reducer into different smaller reducers, but we use combineReducers() to combine them

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

# HTML
## HTML Semantic
Semantic HTML is HTML that introduces meaning to the web page rather than just presentation. For example, a <p> tag indicates that the enclosed text is a paragraph. This is both semantic and presentational, because people know what paragraphs are and browsers know how to display them. In HTML4, tags like <b> and <i> are not semantic, because they define only how the text should look (bold or italic) and do not provide any additional meaning.
Examples of semantic HTML tags include the header tags '<h1> through <h6>, <blockquote>, <code> and <em>'. There are many more semantic HTML tags.

### Why Semantic HTML is Important
1. semantic code aids accessibility. Specially, many people whose eyes are not good rely on speech browsers to read pages to them. These programs cannot interpret pages very well unless they are clearly explained.
2. Help Search engines to better understand pages.  Search engine need to understand what your content is about when rank you properly on search engines. Semantic code tends to improve your placement on search engines, as it is easier for the "search engine spiders" to understand.
3. It’s easier to read and edit, which saves time and money during maintenance.

# Http

## Features of Http
1. connectionless
2. data type independent
3. stateless

## Post VS Get



# Browser

## What is CORS?

Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers to tell a browser to let a web application running at one origin (domain) have permission to access selected resources from a server at a different origin.

## How to cross origin?
1. CORS mechanism: it is decided by server of the requested source(the server decides Access-Control-Allow-Origin)
2. JSONP
3. proxy server

## Event delegation:
add a event listener to a single common parent rather than each child, based on the event bubbling mechanism

https://www.cnblogs.com/bfgis/p/5460191.html

## event flow
1. event  flow  includes capture phase, target phase and bubble phase.
2.	Capturing phase – the event goes down to the element.
3.	Target phase – the event reached the target element.
4.	Bubbling phase – the event bubbles up from the element
5.  capture and bubble phase are event propagation
6. we can use stopPropogation to stop

# General Web question

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
