# Polyfill for filter

## Problem

Implement a polyfill for the `Array.prototype.filter` method. A polyfill is a piece of code that provides the functionality of a modern feature on older browsers that do not support it.

## Solution

The `filter` method creates a new array with all elements that pass the test implemented by the provided function.

```javascript
if (!Array.prototype.filter) {
  Array.prototype.filter = function(callback, thisArg) {
    if (this == null) {
      throw new TypeError('this is null or not defined');
    }
    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }

    const arr = Object(this);
    const len = arr.length >>> 0;
    const newArr = [];
    
    for (let i = 0; i < len; i++) {
      if (i in arr) {
        if (callback.call(thisArg, arr[i], i, arr)) {
          newArr.push(arr[i]);
        }
      }
    }
    
    return newArr;
  };
}

// Example
const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // [2, 4, 6]
```
