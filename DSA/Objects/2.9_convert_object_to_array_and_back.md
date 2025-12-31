# Convert Object to Array and Back

## Problem

Write functions to convert an object to an array of key-value pairs, and a function to convert an array of key-value pairs back to an object.

## Solution

### Object to Array

We can use `Object.entries()` to get an array of a given object's own enumerable string-keyed property [key, value] pairs.

```javascript
function objectToArray(obj) {
  return Object.entries(obj);
}

// Example
const obj = { a: 1, b: 2 };
const arr = objectToArray(obj);
console.log(arr); // [['a', 1], ['b', 2]]
```

### Array to Object

We can use `Object.fromEntries()` to convert a list of key-value pairs into an object.

```javascript
function arrayToObject(arr) {
  return Object.fromEntries(arr);
}

// Example
const arr = [['a', 1], ['b', 2]];
const obj = arrayToObject(arr);
console.log(obj); // { a: 1, b: 2 }
```
