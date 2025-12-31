# Convert Array to Object Using a Key

## Problem

Given an array of objects, convert it into an object where the keys are the values of a specified property from the objects in the array.

## Solution

We can use `reduce` to iterate over the array and build the new object.

```javascript
function arrayToObject(arr, key) {
  return arr.reduce((obj, item) => {
    obj[item[key]] = item;
    return obj;
  }, {});
}

// Example
const people = [
  { id: 1, name: 'Alice', age: 30 },
  { id: 2, name: 'Bob', age: 25 },
  { id: 3, name: 'Charlie', age: 35 }
];

const peopleById = arrayToObject(people, 'id');
console.log(peopleById);
// {
//   '1': { id: 1, name: 'Alice', age: 30 },
//   '2': { id: 2, name: 'Bob', age: 25 },
//   '3': { id: 3, name: 'Charlie', age: 35 }
// }
```
