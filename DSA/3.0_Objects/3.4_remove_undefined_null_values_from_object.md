# Remove Undefined / Null Values from Object

## Problem

Given an object, write a function to remove all properties that have `null` or `undefined` values. This should also work for nested objects.

## Solution

We can write a recursive function that creates a new object, only including properties that do not have `null` or `undefined` values.

```javascript
function removeNullUndefined(obj) {
  if (Array.isArray(obj)) {
    return obj.map(removeNullUndefined).filter(v => v !== null && v !== undefined);
  } else if (obj !== null && obj.constructor === Object) {
    return Object.keys(obj).reduce((result, key) => {
      const value = removeNullUndefined(obj[key]);
      if (value !== null && value !== undefined) {
        result[key] = value;
      }
      return result;
    }, {});
  }
  return obj;
}

// Example
const dirtyObject = {
  a: 1,
  b: null,
  c: undefined,
  d: {
    e: 'hello',
    f: null
  },
  g: [1, undefined, 3]
};

const cleanObject = removeNullUndefined(dirtyObject);
console.log(cleanObject);
// {
//   a: 1,
//   d: {
//     e: 'hello'
//   },
//   g: [1, 3]
// }
```
