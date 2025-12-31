# Quick Sort

## Problem

Implement the Quick Sort algorithm to sort an array of numbers in ascending order. Quick Sort is an efficient, comparison-based sorting algorithm that uses a divide-and-conquer strategy.

## Solution

The main idea behind Quick Sort is to pick an element as a pivot and partition the array around the picked pivot.

```javascript
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const pivot = arr[Math.floor(arr.length / 2)];
  const left = [];
  const right = [];
  const equals = [];

  for (const element of arr) {
    if (element < pivot) {
      left.push(element);
    } else if (element > pivot) {
      right.push(element);
    } else {
      equals.push(element);
    }
  }

  return [...quickSort(left), ...equals, ...quickSort(right)];
}

// Example
const unsortedArray = [10, 7, 8, 9, 1, 5];
const sortedArray = quickSort(unsortedArray);
console.log(sortedArray); // [1, 5, 7, 8, 9, 10]
```
