# Custom Promise.race

## Problem

Implement a function `customPromiseRace` that mimics the behavior of `Promise.race`. It should take an array of promises and return a new promise that resolves or rejects as soon as one of the promises in the iterable resolves or rejects, with the value or reason from that promise.

## Solution

```javascript
function customPromiseRace(promises) {
  return new Promise((resolve, reject) => {
    promises.forEach(promise => {
      Promise.resolve(promise).then(resolve, reject);
    });
  });
}

// Example
const p1 = new Promise((resolve, reject) => {
  setTimeout(resolve, 500, 'one');
});

const p2 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'two');
});

customPromiseRace([p1, p2]).then(value => {
  console.log(value); // "two"
});

const p3 = new Promise((resolve, reject) => {
    setTimeout(reject, 200, 'three');
});

customPromiseRace([p1, p3]).then(value => {
    console.log(value);
}).catch(error => {
    console.error(error); // "three"
});
```
