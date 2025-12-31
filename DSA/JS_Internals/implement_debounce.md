# Implement Debounce

## Problem

Implement a `debounce` function. Debouncing is a technique to limit the rate at which a function gets called. The `debounce` function should take a function and a delay time, and return a new function that will only call the original function after the delay has passed without any new calls.

## Solution

```javascript
function debounce(func, delay) {
  let timeoutId;

  return function(...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => {
      func.apply(this, args);
    }, delay);
  };
}

// Example
function handleInput(value) {
  console.log(`Searching for: ${value}`);
}

const debouncedHandleInput = debounce(handleInput, 500);

// In a browser environment, you would attach this to an input event:
// const inputElement = document.getElementById('search-input');
// inputElement.addEventListener('input', (e) => {
//   debouncedHandleInput(e.target.value);
// });

// Simulating fast input
debouncedHandleInput('h');
debouncedHandleInput('he');
debouncedHandleInput('hel');
debouncedHandleInput('hell');
debouncedHandleInput('hello');

// Only the last call will trigger the console.log after 500ms
```
