# Find Intersection of Two Arrays

## Problem

Given two arrays, write a function to compute their intersection. The intersection consists of elements that are common to both arrays.

## Solution

We can use a `Set` for efficient lookup. We'll create a `Set` from the first array and then filter the second array, keeping only the elements that are present in the `Set`.

```javascript
function findIntersection(arr1, arr2) {
  const set1 = new Set(arr1);
  return arr2.filter(element => set1.has(element));
}

// Example
const array1 = [1, 2, 3, 4, 5];
const array2 = [3, 4, 5, 6, 7];
const intersection = findIntersection(array1, array2);
console.log(intersection); // [3, 4, 5]
```
