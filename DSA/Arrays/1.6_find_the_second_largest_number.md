# Find the Second Largest Number

## Problem

Given an array of numbers, write a function to find the second largest number in the array.

## Solution

We can iterate through the array keeping track of the largest and second largest numbers found so far.

```javascript
function findSecondLargest(arr) {
  let largest = -Infinity;
  let secondLargest = -Infinity;

  for (const num of arr) {
    if (num > largest) {
      secondLargest = largest;
      largest = num;
    } else if (num > secondLargest && num < largest) {
      secondLargest = num;
    }
  }

  return secondLargest;
}

// Example
const numbers = [10, 5, 8, 20, 15];
const secondLargest = findSecondLargest(numbers);
console.log(secondLargest); // 15
```
