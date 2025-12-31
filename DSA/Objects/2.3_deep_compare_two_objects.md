# Deep Compare Two Objects

## Problem

Write a function that deeply compares two objects for equality. The function should return `true` if the objects have the same keys with the same values, and `false` otherwise. This includes nested objects and arrays.

## Solution

We can write a recursive function to handle deep comparison. We need to handle primitives, objects, and arrays.

```javascript
function deepCompare(obj1, obj2) {
  // Check if types and values of primitives are same
  if (obj1 === obj2) {
    return true;
  }

  // Check if one is object and other is not
  if (typeof obj1 !== 'object' || obj1 === null || typeof obj2 !== 'object' || obj2 === null) {
    return false;
  }

  // Get keys of both objects
  const keys1 = Object.keys(obj1);
  const keys2 = Object.keys(obj2);

  // Check if number of keys are same
  if (keys1.length !== keys2.length) {
    return false;
  }

  // Check if all keys and values are same
  for (const key of keys1) {
    if (!keys2.includes(key) || !deepCompare(obj1[key], obj2[key])) {
      return false;
    }
  }

  return true;
}

// Example
const objA = { a: 1, b: { c: 2 } };
const objB = { a: 1, b: { c: 2 } };
const objC = { a: 1, b: { c: 3 } };

console.log(deepCompare(objA, objB)); // true
console.log(deepCompare(objA, objC)); // false
```
