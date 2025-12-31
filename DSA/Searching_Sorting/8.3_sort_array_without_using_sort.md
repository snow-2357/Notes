# Sort Array Without Using .sort()

## Problem

Implement a sorting algorithm to sort an array of numbers in ascending order without using the built-in `Array.prototype.sort()` method.

## Solution (Selection Sort)

One simple sorting algorithm is Selection Sort. It works by repeatedly finding the minimum element from the unsorted part of the array and putting it at the beginning.

```javascript
function selectionSort(arr) {
  const n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    let minIndex = i;
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }
    // Swap the found minimum element with the first element
    if (minIndex !== i) {
      [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
    }
  }
  return arr;
}

// Example
const unsortedArray = [64, 25, 12, 22, 11];
selectionSort(unsortedArray);
console.log(unsortedArray); // [11, 12, 22, 25, 64]
```

## Solution (Insertion Sort)

Another simple sorting algorithm is Insertion Sort. It builds the final sorted array one item at a time. It iterates through the input elements and grows a sorted output list. At each iteration, Insertion Sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there.

```javascript
function insertionSort(arr) {
  const n = arr.length;

  for (let i = 1; i < n; i++) {
    let current = arr[i];
    let j = i - 1;

    // Move elements of arr[0..i-1], that are greater than current,
    // to one position ahead of their current position
    while (j >= 0 && arr[j] > current) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = current;
  }
  return arr;
}

// Example
const unsortedArray2 = [12, 11, 13, 5, 6];
insertionSort(unsortedArray2);
console.log(unsortedArray2); // [5, 6, 11, 12, 13]
```
