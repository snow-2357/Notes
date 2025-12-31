# Bubble Sort

## Problem

Implement the Bubble Sort algorithm to sort an array of numbers in ascending order. Bubble Sort is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements and swaps them if they are in the wrong order.

## Solution

```javascript
function bubbleSort(arr) {
  const n = arr.length;
  for (let i = 0; i < n - 1; i++) {
    for (let j = 0; j < n - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        // swap
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }
  return arr;
}

// Example
const unsortedArray = [64, 34, 25, 12, 22, 11, 90];
bubbleSort(unsortedArray);
console.log(unsortedArray); // [11, 12, 22, 25, 34, 64, 90]
```
*Note: Bubble sort is not a practical sorting algorithm for large datasets as its average and worst-case time complexity are O(n^2).*
