# Linear Search

## Problem

Given an array and a target value, write a function to find the index of the target in the array using linear search. If the target is not found, return -1.

## Solution

Linear search is the simplest search algorithm. It sequentially checks each element of the list until a match is found or the whole list has been searched.

```javascript
function linearSearch(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
      return i; // Target found at index i
    }
  }
  return -1; // Target not found
}

// Example
const array = [5, 2, 8, 12, 1, 9];
console.log(linearSearch(array, 8));  // 2
console.log(linearSearch(array, 10)); // -1
```
