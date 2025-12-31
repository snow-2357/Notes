# Find Object with Max / Min Value

## Problem

Given an array of objects and a key, write functions to find the object with the maximum and minimum value for that key.

## Solution

We can use `reduce` to iterate through the array and keep track of the object with the max or min value found so far.

### Find Object with Max Value

```javascript
function findObjectWithMaxValue(arr, key) {
  if (arr.length === 0) {
    return null;
  }
  return arr.reduce((maxObj, currentObj) => {
    return currentObj[key] > maxObj[key] ? currentObj : maxObj;
  });
}

// Example
const people = [
  { name: 'Alice', age: 30 },
  { name: 'Bob', age: 25 },
  { name: 'Charlie', age: 35 }
];

const oldestPerson = findObjectWithMaxValue(people, 'age');
console.log(oldestPerson); // { name: 'Charlie', age: 35 }
```

### Find Object with Min Value

```javascript
function findObjectWithMinValue(arr, key) {
  if (arr.length === 0) {
    return null;
  }
  return arr.reduce((minObj, currentObj) => {
    return currentObj[key] < minObj[key] ? currentObj : minObj;
  });
}

// Example
const youngestPerson = findObjectWithMinValue(people, 'age');
console.log(youngestPerson); // { name: 'Bob', age: 25 }
```
