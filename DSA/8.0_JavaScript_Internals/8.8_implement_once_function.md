# Implement once() Function

## Problem

Write a function `once` that takes a function and returns a new function. The new function should only be able to be called once. Subsequent calls should not invoke the original function and should return the result of the first call.

## Solution

```javascript
function once(fn) {
  let hasBeenCalled = false;
  let result;

  return function(...args) {
    if (!hasBeenCalled) {
      hasBeenCalled = true;
      result = fn.apply(this, args);
      return result;
    }
    return result;
  };
}

// Example
function initializePayment() {
  console.log('Initializing payment...');
  return { success: true };
}

const initializeOnce = once(initializePayment);

const result1 = initializeOnce(); // 'Initializing payment...' will be logged
const result2 = initializeOnce(); // Nothing will be logged

console.log(result1); // { success: true }
console.log(result2); // { success: true }
```
