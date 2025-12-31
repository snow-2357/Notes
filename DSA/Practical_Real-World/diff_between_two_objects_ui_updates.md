# Diff Between Two Objects (UI Updates)

## Problem

When updating a UI, it's often more efficient to apply only the changes rather than re-rendering the entire component. Write a function that takes two objects (an old state and a new state) and returns an object representing the differences, suitable for applying minimal UI updates. This function should focus on properties that have changed, been added, or been removed.

## Solution

We can iterate through the keys of both objects and compare their values. This is a shallow diff. For a deep diff, it would involve recursion.

```javascript
function getObjectDiff(oldObj, newObj) {
  const diff = {};

  // Check for changed or added properties
  for (const key in newObj) {
    if (newObj.hasOwnProperty(key)) {
      if (!oldObj.hasOwnProperty(key) || oldObj[key] !== newObj[key]) {
        diff[key] = newObj[key];
      }
    }
  }

  // Check for removed properties
  for (const key in oldObj) {
    if (oldObj.hasOwnProperty(key)) {
      if (!newObj.hasOwnProperty(key)) {
        diff[key] = undefined; // Mark as removed
      }
    }
  }

  return diff;
}

// Example
const oldState = {
  id: 1,
  name: 'Alice',
  age: 30,
  city: 'New York'
};

const newState = {
  id: 1,
  name: 'Alicia', // Changed
  age: 30,
  country: 'USA' // Added
};

const changes = getObjectDiff(oldState, newState);
console.log(changes);
// {
//   name: 'Alicia',
//   country: 'USA',
//   city: undefined // 'city' was removed from newState
// }

const oldStateDeep = {
    a: 1,
    b: { c: 2, d: 3 },
    e: [1, 2]
};

const newStateDeep = {
    a: 1,
    b: { c: 2, d: 4 }, // d changed
    e: [1, 2, 3] // e changed
};

// This shallow diff won't catch nested changes effectively without further logic.
// A full deep diff library would be needed for recursive comparison.
const deepChanges = getObjectDiff(oldStateDeep, newStateDeep);
console.log(deepChanges);
// {
//   "b": { "c": 2, "d": 4 }, // "b" is seen as changed because the object reference is different or its content is not deeply compared
//   "e": [1, 2, 3]  // "e" is seen as changed
// }
```
