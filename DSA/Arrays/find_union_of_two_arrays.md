# Find Union of Two Arrays

## Problem

Given two arrays, write a function to compute their union. The union of two sets is a set containing all elements from both sets, with duplicates removed.

## Solution

We can combine both arrays and then use a `Set` to automatically handle the removal of duplicates.

```javascript
function findUnion(arr1, arr2) {
  const combinedArray = [...arr1, ...arr2];
  return [...new Set(combinedArray)];
}

// Example
const array1 = [1, 2, 3, 4, 5];
const array2 = [3, 4, 5, 6, 7];
const union = findUnion(array1, array2);
console.log(union); // [1, 2, 3, 4, 5, 6, 7]
```
