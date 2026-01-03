# Remove Duplicate Objects by Id

## Problem

Given an array of objects, remove duplicate objects based on a specific key, like `id`. The first occurrence of an object with a given `id` should be kept.

## Solution

We can use a `Set` to keep track of the `id`s we've already seen, and `filter` to build the new array.

```javascript
function removeDuplicateObjects(arr, key) {
  const seen = new Set();
  return arr.filter(obj => {
    const keyValue = obj[key];
    if (seen.has(keyValue)) {
      return false;
    } else {
      seen.add(keyValue);
      return true;
    }
  });
}

// Example
const arrayWithDuplicates = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' },
  { id: 1, name: 'Alicia' },
  { id: 3, name: 'Charlie' }
];

const uniqueArray = removeDuplicateObjects(arrayWithDuplicates, 'id');
console.log(uniqueArray);
// [
//   { id: 1, name: 'Alice' },
//   { id: 2, name: 'Bob' },
//   { id: 3, name: 'Charlie' }
// ]
```
