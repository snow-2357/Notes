# Search in Rotated Sorted Array

## Problem

Given a sorted array that has been rotated at some pivot point (e.g., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`), and a target value, write a function to find the index of the target in the array. If the target is not found, return -1. Assume there are no duplicate elements.

## Solution

This problem can be solved using a modified binary search approach. The key is to determine which half of the array is sorted and then decide whether to search in that sorted half or the other (unsorted) half.

```javascript
function searchInRotatedSortedArray(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      return mid;
    }

    // Determine which half is sorted
    if (arr[left] <= arr[mid]) { // Left half is sorted
      if (target >= arr[left] && target < arr[mid]) {
        right = mid - 1; // Target is in the sorted left half
      } else {
        left = mid + 1; // Target is in the unsorted right half
      }
    } else { // Right half is sorted
      if (target > arr[mid] && target <= arr[right]) {
        left = mid + 1; // Target is in the sorted right half
      } else {
        right = mid - 1; // Target is in the unsorted left half
      }
    }
  }

  return -1; // Target not found
}

// Example
const rotatedArray = [4, 5, 6, 7, 0, 1, 2];
console.log(searchInRotatedSortedArray(rotatedArray, 0)); // 4
console.log(searchInRotatedSortedArray(rotatedArray, 3)); // -1

const rotatedArray2 = [6, 7, 0, 1, 2, 3, 4, 5];
console.log(searchInRotatedSortedArray(rotatedArray2, 7)); // 1
```
