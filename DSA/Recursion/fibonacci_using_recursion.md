# Fibonacci Using Recursion

## Problem

Write a recursive function to return the nth number in the Fibonacci sequence. The Fibonacci sequence is a series of numbers in which each number is the sum of the two preceding ones, usually starting with 0 and 1.

## Solution

The base cases for the recursion are for n=0 and n=1. For any other `n`, the Fibonacci number is the sum of the (n-1)th and (n-2)th Fibonacci numbers.

```javascript
function fibonacci(n) {
  if (n < 0) {
      return "Input must be a non-negative integer";
  }
  if (n === 0) {
    return 0;
  }
  if (n === 1) {
    return 1;
  }
  return fibonacci(n - 1) + fibonacci(n - 2);
}

// Example
console.log(fibonacci(7)); // 13 (0, 1, 1, 2, 3, 5, 8, 13)
```

### Memoization for Optimization

The simple recursive solution is inefficient because it recalculates the same Fibonacci numbers multiple times. We can optimize this using memoization (caching the results).

```javascript
function fibonacciMemo(n, memo = {}) {
    if (n < 0) {
        return "Input must be a non-negative integer";
    }
    if (n in memo) {
        return memo[n];
    }
    if (n === 0) {
        return 0;
    }
    if (n === 1) {
        return 1;
    }

    memo[n] = fibonacciMemo(n - 1, memo) + fibonacciMemo(n - 2, memo);
    return memo[n];
}

// Example
console.log(fibonacciMemo(50)); // 12586269025
```
This version is much faster for larger values of `n`.
