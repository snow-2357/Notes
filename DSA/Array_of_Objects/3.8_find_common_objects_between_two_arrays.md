# Find Common Objects Between Two Arrays

## Problem

Given two arrays of objects, find the objects that are present in both arrays. The comparison should be based on a specific property, like `id`.

## Solution

We can create a `Set` of the `id`s from the first array for efficient lookup. Then, we can filter the second array, keeping only the objects whose `id` is in the `Set`.

```javascript
function findCommonObjects(arr1, arr2, key) {
  const keySet = new Set(arr1.map(obj => obj[key]));
  return arr2.filter(obj => keySet.has(obj[key]));
}

// Example
const arr1 = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' },
  { id: 3, name: 'Charlie' }
];

const arr2 = [
  { id: 2, name: 'Bob' },
  { id: 3, name: 'Charlie' },
  { id: 4, name: 'David' }
];

const commonObjects = findCommonObjects(arr1, arr2, 'id');
console.log(commonObjects);
// [
//   { id: 2, name: 'Bob' },
//   { id: 3, name: 'Charlie' }
// ]
```
