# Sum of Digits using Recursion

## Problem

Write a recursive function to calculate the sum of the digits of a non-negative integer.

## Solution

We can solve this by taking the number modulo 10 to get the last digit, and then making a recursive call with the rest of the number (the number divided by 10, integer part). The base case is when the number is 0.

```javascript
function sumOfDigits(n) {
  n = Math.abs(Math.floor(n)); // handle non-negative integers

  if (n === 0) {
    return 0;
  }
  return (n % 10) + sumOfDigits(Math.floor(n / 10));
}

// Example
console.log(sumOfDigits(12345)); // 15
console.log(sumOfDigits(987));   // 24
```
