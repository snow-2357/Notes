# Resolve Nested Promises Recursively

## Problem

Write a function that takes a deeply nested promise (a promise that resolves to another promise, which may resolve to another, and so on) and recursively resolves it until a non-promise value is found.

## Solution

We can write a function that takes a promise. It uses `.then()` to get the resolved value. If the resolved value is another promise, it makes a recursive call. Otherwise, it returns the value.

```javascript
function resolveNestedPromise(promise) {
  return promise.then(result => {
    if (result instanceof Promise) {
      return resolveNestedPromise(result);
    }
    return result;
  });
}

// Example
const p1 = Promise.resolve('final value');
const p2 = Promise.resolve(p1);
const p3 = Promise.resolve(p2);

resolveNestedPromise(p3).then(value => {
  console.log(value); // 'final value'
});
```
