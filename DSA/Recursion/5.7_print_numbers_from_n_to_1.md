# Print Numbers from N to 1 using Recursion

## Problem

Write a recursive function that takes an integer `n` and prints numbers from `n` down to 1.

## Solution

The base case for the recursion is when `n` is 0. For any other positive integer `n`, we print the number and then make a recursive call for `n-1`.

```javascript
function printNto1(n) {
  if (n <= 0) {
    return;
  }
  console.log(n);
  printNto1(n - 1);
}

// Example
printNto1(5);
// 5
// 4
// 3
// 2
// 1
```
