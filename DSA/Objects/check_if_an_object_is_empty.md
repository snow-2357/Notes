# Check if an Object is Empty

## Problem

Given an object, write a function to check if it is empty. An object is considered empty if it has no own properties.

## Solution

We can use `Object.keys()` to get an array of the object's own enumerable property names. If the length of this array is 0, the object is empty.

```javascript
function isObjectEmpty(obj) {
  return Object.keys(obj).length === 0;
}

// Example
const emptyObject = {};
const nonEmptyObject = { a: 1 };

console.log(isObjectEmpty(emptyObject)); // true
console.log(isObjectEmpty(nonEmptyObject)); // false
```
