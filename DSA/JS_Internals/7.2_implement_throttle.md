# Implement Throttle

## Problem

Implement a `throttle` function. Throttling is a technique to limit a function to be called at most once in a given time interval. The `throttle` function should take a function and a time limit, and return a new function that will call the original function at most once per the specified time limit.

## Solution

```javascript
function throttle(func, limit) {
  let inThrottle;
  let lastFunc;
  let lastRan;
  return function() {
    const context = this;
    const args = arguments;
    if (!inThrottle) {
      func.apply(context, args);
      lastRan = Date.now();
      inThrottle = true;
    } else {
      clearTimeout(lastFunc);
      lastFunc = setTimeout(function() {
        if ((Date.now() - lastRan) >= limit) {
          func.apply(context, args);
          lastRan = Date.now();
        }
      }, limit - (Date.now() - lastRan));
    }
  }
}

// Example
function onScroll() {
  console.log('Scroll event fired!');
}

const throttledOnScroll = throttle(onScroll, 1000);

// In a browser environment, you would attach this to a scroll event:
// window.addEventListener('scroll', throttledOnScroll);

// Simulating fast scroll events
throttledOnScroll(); // Fires immediately
throttledOnScroll(); // Ignored
throttledOnScroll(); // Ignored

// After 1 second, the next call would fire.
setTimeout(() => {
    throttledOnScroll(); // Fires
}, 1100);

```
