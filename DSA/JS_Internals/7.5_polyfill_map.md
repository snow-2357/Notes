# Polyfill for map

## Problem

Implement a polyfill for the `Array.prototype.map` method. A polyfill is a piece of code that provides the functionality of a modern feature on older browsers that do not support it.

## Solution

The `map` method creates a new array populated with the results of calling a provided function on every element in the calling array.

```javascript
if (!Array.prototype.map) {
  Array.prototype.map = function(callback, thisArg) {
    if (this == null) {
      throw new TypeError('this is null or not defined');
    }
    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }

    const arr = Object(this);
    const len = arr.length >>> 0;
    const newArr = new Array(len);
    
    for (let i = 0; i < len; i++) {
      if (i in arr) {
        newArr[i] = callback.call(thisArg, arr[i], i, arr);
      }
    }
    
    return newArr;
  };
}

// Example
const numbers = [1, 2, 3];
const doubledNumbers = numbers.map(num => num * 2);
console.log(doubledNumbers); // [2, 4, 6]
```
