# Find the Missing Number in 1 to N

## Problem

Given an array containing n distinct numbers taken from the range 1 to n+1, find the one that is missing from the array.

## Solution

The sum of numbers from 1 to n is given by the formula `n * (n + 1) / 2`. We can calculate the expected sum and subtract the actual sum of the elements in the array to find the missing number.

```javascript
function findMissingNumber(arr) {
  const n = arr.length + 1;
  const expectedSum = n * (n + 1) / 2;
  const actualSum = arr.reduce((sum, num) => sum + num, 0);
  return expectedSum - actualSum;
}

// Example
const numbers = [1, 2, 4, 5, 6];
const missingNumber = findMissingNumber(numbers);
console.log(missingNumber); // 3
```
