# Common front-end questions

1.	the forEach() method doesn’t actually return anything (undefined). It simply calls a provided function on each element in your array. This callback is allowed to mutate the calling array.However, the map() method will also call a provided function on every element in the array. The difference is that map() utilizes return values and actually returns a new Array of the same size.
##	forEach() VS map()
2.	forEach can be used by map, set and array, map just be used by array

## What is a Closure?

A closure is an inner function that has access to the outer function’s variables.

## What is CORS?

Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers to tell a browser to let a web application running at one origin (domain) have permission to access selected resources from a server at a different origin.

## How to cross origin?
1. CORS mechanism: it is decidedy by server of the requested source(the server decides Access-Control-Allow-Origin)
2. JSONP
3. proxy server

## The way to judge the data type  in js
Object.prototype.toString.call();
jquery.type();

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
