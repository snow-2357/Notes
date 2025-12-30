# Flatten a Deeply Nested Array

## Problem

Given a deeply nested array, write a function to flatten it into a single-level array.

## Solution

We can solve this recursively. We'll create a function that iterates through the array. If an element is an array itself, we'll recursively call the function on that element. Otherwise, we'll push the element into our flattened array.

```javascript
function flattenDeeplyNestedArray(arr) {
  const flattened = [];

  function flatten(element) {
    if (Array.isArray(element)) {
      for (const item of element) {
        flatten(item);
      }
    } else {
      flattened.push(element);
    }
  }

  flatten(arr);
  return flattened;
}

// Example
const nestedArray = [1, [2, [3, [4, 5]], 6], 7];
const flattenedArray = flattenDeeplyNestedArray(nestedArray);
console.log(flattenedArray); // [1, 2, 3, 4, 5, 6, 7]
```

### Using `Array.prototype.flat()`

ES2019 introduced the `flat()` method, which makes this task trivial. You can provide a depth to flatten, or use `Infinity` to flatten all levels.

```javascript
function flattenWithFlat(arr) {
  return arr.flat(Infinity);
}

// Example
const nestedArray = [1, [2, [3, [4, 5]], 6], 7];
const flattenedArray = flattenWithFlat(nestedArray);
console.log(flattenedArray); // [1, 2, 3, 4, 5, 6, 7]
```
