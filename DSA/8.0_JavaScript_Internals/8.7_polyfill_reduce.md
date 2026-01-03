# Polyfill for reduce

## Problem

Implement a polyfill for the `Array.prototype.reduce` method. A polyfill is a piece of code that provides the functionality of a modern feature on older browsers that do not support it.

## Solution

The `reduce` method executes a user-supplied "reducer" callback function on each element of the array, in order, passing in the return value from the calculation on the preceding element. The final result of running the reducer across all elements of the array is a single value.

```javascript
if (!Array.prototype.reduce) {
  Array.prototype.reduce = function(callback /*, initialValue*/) {
    if (this == null) {
      throw new TypeError('this is null or not defined');
    }
    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }

    const arr = Object(this);
    const len = arr.length >>> 0;
    let i = 0;
    let accumulator;

    if (arguments.length >= 2) {
      accumulator = arguments[1];
    } else {
      while (i < len && !(i in arr)) {
        i++;
      }
      if (i >= len) {
        throw new TypeError('Reduce of empty array with no initial value');
      }
      accumulator = arr[i++];
    }
    
    for (; i < len; i++) {
      if (i in arr) {
        accumulator = callback(accumulator, arr[i], i, arr);
      }
    }
    
    return accumulator;
  };
}

// Example
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, curr) => acc + curr, 0);
console.log(sum); // 10
```
