# Find a Key Inside a Nested Object

## Problem

Write a function that searches for a given key in a nested object and returns its value. If the key is not found, it should return `undefined`.

## Solution

We can use a recursive approach to traverse the nested object and find the key.

```javascript
function findKeyInNestedObject(obj, keyToFind) {
  for (const key in obj) {
    if (key === keyToFind) {
      return obj[key];
    }
    if (typeof obj[key] === 'object' && obj[key] !== null) {
      const result = findKeyInNestedObject(obj[key], keyToFind);
      if (result !== undefined) {
        return result;
      }
    }
  }
  return undefined;
}

// Example
const nestedObject = {
  a: 1,
  b: {
    c: 2,
    d: {
      e: 3,
      f: 4
    }
  }
};

console.log(findKeyInNestedObject(nestedObject, 'e')); // 3
console.log(findKeyInNestedObject(nestedObject, 'g')); // undefined
```
