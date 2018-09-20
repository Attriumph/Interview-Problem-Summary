# Common front-end questions

##	forEach() VS map()
1.	the forEach() method doesn’t return anything (undefined). It simply calls a provided function on each element in your array. However, the map() method will also call a provided function on every element in the array and returns a new Array of the same size.
2.	forEach can be used by map, set and array, map just be used by array

## What is a Closure?

A closure is an inner function that has access to the outer function’s variables.

## What is CORS?

Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers to tell a browser to let a web application running at one origin (domain) have permission to access selected resources from a server at a different origin.

## How to cross origin?
1. CORS mechanism: it is decided by server of the requested source(the server decides Access-Control-Allow-Origin)
2. JSONP
3. proxy server

## The way to judge the data type  in js
Object.prototype.toString.call(), return [Object，type]
jquery.type();

## What is Promise?
Since JavaScript is single-thread language, so we need a lot of asynchronous functions. However, sometime we got a bunch of nested code for asynchronous operation. Therefore, we introduce Promise to solve this problem.

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

## apply() vs call()
Both these functions are used to bind this to functions. JavaScript function has their owner.
The only difference is parameters for them. The call() method takes arguments separately.
The apply() method takes arguments as an array.

## Event delegation:
https://www.cnblogs.com/bfgis/p/5460191.html
event  flow  includes capture phase, target phase and bubble phase.

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

## Features of Http
1. connectionless
2. data type independent
3. stateless

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
