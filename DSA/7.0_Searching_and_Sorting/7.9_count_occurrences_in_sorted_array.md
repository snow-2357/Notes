# Count Occurrences in Sorted Array

## Problem

Given a sorted array and a target value, write a function to count the number of times the target value appears in the array.

## Solution

Since the array is sorted, we can use binary search to find the first and last occurrence of the target value. Once we have the indices of the first and last occurrences, the count is simply `lastIndex - firstIndex + 1`.

```javascript
// Helper function to find the first occurrence of the target
function findFirstOccurrence(arr, target) {
  let low = 0;
  let high = arr.length - 1;
  let result = -1;

  while (low <= high) {
    const mid = Math.floor((low + high) / 2);
    if (arr[mid] === target) {
      result = mid;
      high = mid - 1; // Look in the left half for an even earlier occurrence
    } else if (arr[mid] < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }
  return result;
}

// Helper function to find the last occurrence of the target
function findLastOccurrence(arr, target) {
  let low = 0;
  let high = arr.length - 1;
  let result = -1;

  while (low <= high) {
    const mid = Math.floor((low + high) / 2);
    if (arr[mid] === target) {
      result = mid;
      low = mid + 1; // Look in the right half for an even later occurrence
    } else if (arr[mid] < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }
  return result;
}

function countOccurrences(arr, target) {
  const firstIndex = findFirstOccurrence(arr, target);
  if (firstIndex === -1) {
    return 0; // Target not found
  }
  const lastIndex = findLastOccurrence(arr, target);
  return lastIndex - firstIndex + 1;
}

// Example
const sortedArray = [1, 2, 3, 3, 3, 4, 5, 5];
console.log(countOccurrences(sortedArray, 3)); // 3
console.log(countOccurrences(sortedArray, 5)); // 2
console.log(countOccurrences(sortedArray, 6)); // 0
```
