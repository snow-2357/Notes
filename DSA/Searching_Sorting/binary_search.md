# Binary Search

## Problem

Given a sorted array of numbers and a target value, write a function to find the index of the target in the array. If the target is not found, return -1. Binary search is a search algorithm that finds the position of a target value within a sorted array.

## Solution

Binary search works by repeatedly dividing the search interval in half.

```javascript
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      return mid;
    } else if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1; // Target not found
}

// Example
const sortedArray = [1, 3, 5, 7, 9, 11, 13];
console.log(binarySearch(sortedArray, 9)); // 4
console.log(binarySearch(sortedArray, 6)); // -1
```
