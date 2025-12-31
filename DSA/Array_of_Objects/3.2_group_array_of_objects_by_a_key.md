# Group Array of Objects by a Key

## Problem

Given an array of objects, group the objects by a specified key. The result should be an object where keys are the unique values of the specified key, and values are arrays of objects that have that key value.

## Solution

We can use `reduce` to iterate over the array and build the grouped object.

```javascript
function groupByKey(arr, key) {
  return arr.reduce((acc, obj) => {
    const keyValue = obj[key];
    if (!acc[keyValue]) {
      acc[keyValue] = [];
    }
    acc[keyValue].push(obj);
    return acc;
  }, {});
}

// Example
const people = [
  { name: 'Alice', age: 30, city: 'New York' },
  { name: 'Bob', age: 25, city: 'Los Angeles' },
  { name: 'Charlie', age: 35, city: 'New York' }
];

const peopleByCity = groupByKey(people, 'city');
console.log(peopleByCity);
// {
//   'New York': [
//     { name: 'Alice', age: 30, city: 'New York' },
//     { name: 'Charlie', age: 35, city: 'New York' }
//   ],
//   'Los Angeles': [
//     { name: 'Bob', age: 25, city: 'Los Angeles' }
//   ]
// }
```
