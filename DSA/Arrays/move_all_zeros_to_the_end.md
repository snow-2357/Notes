# Move All Zeros to the End

## Problem

Given an array of numbers, write a function to move all the zeros to the end of the array, while maintaining the relative order of the non-zero elements.

## Solution

We can iterate through the array with two pointers. One pointer (`nonZeroIndex`) keeps track of where the next non-zero element should be placed. The other pointer (`i`) iterates through the array. When a non-zero element is found, it's placed at `nonZeroIndex` and `nonZeroIndex` is incremented. After the first pass, all non-zero elements are at the beginning of the array in their original relative order. The rest of the array is then filled with zeros.

```javascript
function moveZerosToEnd(arr) {
  let nonZeroIndex = 0;

  // Move all non-zero elements to the front
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] !== 0) {
      arr[nonZeroIndex] = arr[i];
      nonZeroIndex++;
    }
  }

  // Fill the rest of the array with zeros
  for (let i = nonZeroIndex; i < arr.length; i++) {
    arr[i] = 0;
  }

  return arr;
}

// Example
const array = [0, 1, 0, 3, 12];
moveZerosToEnd(array);
console.log(array); // [1, 3, 12, 0, 0]
```
