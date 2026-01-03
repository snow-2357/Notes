# Deep Clone an Object using Recursion

## Problem

Write a recursive function to create a deep clone of an object. A deep clone means that all nested objects and arrays are also cloned, not just referenced.

## Solution

We can write a function that creates a new object or array. Then, it iterates through the keys of the original object. If a value is an object or array, it makes a recursive call to clone it. Otherwise, it copies the primitive value.

```javascript
function deepClone(obj) {
  if (obj === null || typeof obj !== 'object') {
    return obj;
  }

  const clone = Array.isArray(obj) ? [] : {};

  for (const key in obj) {
    clone[key] = deepClone(obj[key]);
  }

  return clone;
}

// Example
const originalObject = {
  a: 1,
  b: {
    c: 2
  },
  d: [1, 2, 3]
};

const clonedObject = deepClone(originalObject);

// Modify the cloned object
clonedObject.b.c = 3;
clonedObject.d.push(4);


console.log(originalObject); // { a: 1, b: { c: 2 }, d: [ 1, 2, 3 ] }
console.log(clonedObject);   // { a: 1, b: { c: 3 }, d: [ 1, 2, 3, 4 ] }
```

*Note: This basic implementation does not handle more complex types like `Date`, `RegExp`, `Map`, `Set`, or functions.*
