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
Object.prototype.toString.call();
jquery.type();

## What is Promise?
Since JavaScript is single-thread language, so we need a lot of asynchronous functions. However, sometime we got a bunch of nested code for asynchronous operation. Therefore, we introduce Promise to solve this problem.

* A Promise object serves as a link between the executor(resolve, reject) and the consuming functions, which will receive the result or error.
* In executor, we do the asynchronous action. After it is done, we will call the consuming functions.
* When the promise is created, this executor function runs automatically. Since it contains the producing code, that will eventually produce a result(consuming function will use the result)
* The resulting promise object has internal properties: state(pending, fulfilled and rejected) and result

* also, we could use '.then' after a promise, so we can control the sequence of a series of asynchronous action
* also, we have promise.all() and promise.race()

## What is generatot?

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
