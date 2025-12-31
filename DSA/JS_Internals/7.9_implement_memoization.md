# Implement Memoization

## Problem

Write a `memoize` function that takes a function and returns a memoized version of it. A memoized function will cache the results of expensive function calls and return the cached result when the same inputs occur again.

## Solution

```javascript
function memoize(fn) {
  const cache = {};
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache[key]) {
      return cache[key];
    } else {
      const result = fn.apply(this, args);
      cache[key] = result;
      return result;
    }
  };
}

// Example
function slowFibonacci(n) {
    if (n < 2) {
        return n;
    }
    return slowFibonacci(n - 1) + slowFibonacci(n - 2);
}

const fastFib = memoize(slowFibonacci);

console.time('fib 40');
console.log(fastFib(40));
console.timeEnd('fib 40');

console.time('fib 40 again');
console.log(fastFib(40));
console.timeEnd('fib 40 again'); // This will be much faster
```
*Note: `JSON.stringify` is a simple way to create a cache key, but it has limitations (e.g., with non-serializable arguments or order of object keys).*
