# Merge Two Deeply Nested Objects

## Problem

Write a function that deeply merges two objects. If a key exists in both objects and their values are objects, the two objects should be merged recursively. Otherwise, the value from the second object should overwrite the value from the first object.

## Solution

We can write a recursive function that iterates through the keys of the source object and merges them into the target object.

```javascript
function deepMerge(target, source) {
  const output = { ...target };

  if (isObject(target) && isObject(source)) {
    Object.keys(source).forEach(key => {
      if (isObject(source[key])) {
        if (!(key in target)) {
          Object.assign(output, { [key]: source[key] });
        } else {
          output[key] = deepMerge(target[key], source[key]);
        }
      } else {
        Object.assign(output, { [key]: source[key] });
      }
    });
  }

  return output;
}

function isObject(item) {
  return (item && typeof item === 'object' && !Array.isArray(item));
}

// Example
const obj1 = {
  a: 1,
  b: {
    c: 2,
    d: {
      e: 3
    }
  }
};

const obj2 = {
  b: {
    d: {
      f: 4
    },
    g: 5
  },
  h: 6
};

const mergedObject = deepMerge(obj1, obj2);
console.log(mergedObject);
// {
//   a: 1,
//   b: {
//     c: 2,
//     d: {
//       e: 3,
//       f: 4
//     },
//     g: 5
//   },
//   h: 6
// }
```
