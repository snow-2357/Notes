# Remove Duplicates from an Array

## Problem

Given an array of primitive values, write a function to return a new array with all duplicate values removed.

## Solution

A straightforward way to solve this is to use a `Set`. A `Set` is a collection of unique values, so it will automatically handle the removal of duplicates.

```javascript
function removeDuplicates(arr) {
  return [...new Set(arr)];
}

// Example
const arrayWithDuplicates = [1, 2, 2, 3, 4, 4, 5];
const uniqueArray = removeDuplicates(arrayWithDuplicates);
console.log(uniqueArray); // [1, 2, 3, 4, 5]
```

### Using `filter()` and `indexOf()`

You can also use the `filter` method. For each element, we check if its first occurrence in the array is at the current index.

```javascript
function removeDuplicatesWithFilter(arr) {
  return arr.filter((item, index) => arr.indexOf(item) === index);
}

// Example
const arrayWithDuplicates = [1, 2, 2, 3, 4, 4, 5];
const uniqueArray = removeDuplicatesWithFilter(arrayWithDuplicates);
console.log(uniqueArray); // [1, 2, 3, 4, 5]
```
