# Count Total Keys in Nested Object using Recursion

## Problem

Write a recursive function to count the total number of keys in a nested object.

## Solution

We can write a function that iterates through the keys of an object. For each key, we increment a counter. If the value associated with a key is another object, we make a recursive call to count the keys in that nested object.

```javascript
function countKeys(obj) {
  let count = 0;
  for (const key in obj) {
    count++;
    if (typeof obj[key] === 'object' && obj[key] !== null) {
      count += countKeys(obj[key]);
    }
  }
  return count;
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
  f: 4
};

console.log(countKeys(nestedObject)); // 6 (a, b, c, d, e, f)
```
