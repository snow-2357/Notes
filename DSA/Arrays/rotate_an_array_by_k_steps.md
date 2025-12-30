# Rotate an Array by k Steps

## Problem

Given an array, rotate the array to the right by k steps, where k is non-negative.

## Solution

We can solve this by using the `splice` and `unshift` methods. We'll remove the last `k` elements from the array and then add them to the beginning.

```javascript
function rotateArray(arr, k) {
  const n = arr.length;
  k = k % n; // to handle cases where k > n

  if (k === 0) {
    return arr;
  }

  const removed = arr.splice(n - k, k);
  arr.unshift(...removed);

  return arr;
}

// Example
const array = [1, 2, 3, 4, 5, 6, 7];
rotateArray(array, 3);
console.log(array); // [5, 6, 7, 1, 2, 3, 4]
```
