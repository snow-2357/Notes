# Find Max Depth of Nested Object/Array using Recursion

## Problem

Write a recursive function to find the maximum depth of a nested object or array. The depth of an element is the number of nested objects or arrays it is inside.

## Solution

We can write a function that takes an object and a current depth. It calculates the depth of each child element by making a recursive call and adding 1. The maximum of these depths is the result.

```javascript
function maxDepth(obj) {
  if (obj === null || typeof obj !== 'object') {
    return 0;
  }

  let depth = 1;
  for (const key in obj) {
    if (typeof obj[key] === 'object' && obj[key] !== null) {
      depth = Math.max(depth, 1 + maxDepth(obj[key]));
    }
  }

  return depth;
}

// Example
const nested = {
  a: 1,
  b: {
    c: 2,
    d: {
      e: 3
    }
  },
  f: [1, [2, [3]]]
};

console.log(maxDepth(nested)); // 4
```
