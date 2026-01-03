# Flatten a Nested Object (Dot Notation)

## Problem

Write a function that flattens a nested object into a single-level object with keys in dot notation.

## Solution

We can use a recursive function to traverse the object. We'll build up the dot notation key as we go deeper into the object.

```javascript
function flattenObject(obj, parentKey = '', result = {}) {
  for (const key in obj) {
    const newKey = parentKey ? `${parentKey}.${key}` : key;
    if (typeof obj[key] === 'object' && obj[key] !== null && !Array.isArray(obj[key])) {
      flattenObject(obj[key], newKey, result);
    } else {
      result[newKey] = obj[key];
    }
  }
  return result;
}

// Example
const nestedObject = {
  a: 1,
  b: {
    c: 2,
    d: {
      e: 3
    }
  },
  f: [1, 2]
};

const flattenedObject = flattenObject(nestedObject);
console.log(flattenedObject);
// {
//   'a': 1,
//   'b.c': 2,
//   'b.d.e': 3,
//   'f': [1, 2]
// }
```
