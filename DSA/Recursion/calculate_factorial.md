# Calculate Factorial using Recursion

## Problem

Write a recursive function to calculate the factorial of a non-negative integer. The factorial of a number `n` (denoted as `n!`) is the product of all positive integers less than or equal to `n`.

## Solution

The base case for the recursion is when `n` is 0, in which case the factorial is 1. For any other positive integer `n`, the factorial is `n` multiplied by the factorial of `n-1`.

```javascript
function factorial(n) {
  if (n < 0) {
    return "Factorial is not defined for negative numbers";
  }
  if (n === 0) {
    return 1;
  }
  return n * factorial(n - 1);
}

// Example
console.log(factorial(5)); // 120 (5 * 4 * 3 * 2 * 1)
console.log(factorial(0)); // 1
```
