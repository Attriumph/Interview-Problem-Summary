# Common front-end questions

1.	the forEach() method doesn’t actually return anything (undefined). It simply calls a provided function on each element in your array. This callback is allowed to mutate the calling array.However, the map() method will also call a provided function on every element in the array. The difference is that map() utilizes return values and actually returns a new Array of the same size.
##	forEach() VS map()
2.	forEach can be used by map, set and array, map just be used by array

## What is a Closure?

A closure is an inner function that has access to the outer function’s variables.

## The way to judge the data type  in js
Object.prototype.toString.call();
jquery.type();

## Event delegation:
https://www.cnblogs.com/bfgis/p/5460191.html
event  flow  includes capture phase, target phase and bubble phase.

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
