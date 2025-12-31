# Find Max Subarray Sum (Kadane's Algorithm)

## Problem

Given an integer array, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

## Solution

This is a classic problem that can be solved efficiently using Kadane's Algorithm. The idea is to iterate through the array and at each position, decide whether it's better to extend the previous subarray or start a new one.

```javascript
function maxSubarraySum(arr) {
  let maxSoFar = -Infinity;
  let maxEndingHere = 0;

  for (let i = 0; i < arr.length; i++) {
    maxEndingHere = maxEndingHere + arr[i];
    if (maxSoFar < maxEndingHere) {
      maxSoFar = maxEndingHere;
    }
    if (maxEndingHere < 0) {
      maxEndingHere = 0;
    }
  }
  return maxSoFar;
}

// Example
const array = [-2, 1, -3, 4, -1, 2, 1, -5, 4];
const maxSum = maxSubarraySum(array);
console.log(maxSum); // 6 (from subarray [4, -1, 2, 1])
```
