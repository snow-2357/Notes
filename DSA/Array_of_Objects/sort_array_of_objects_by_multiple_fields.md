# Sort Array of Objects by Multiple Fields

## Problem

Given an array of objects, write a function to sort the array by multiple fields. The function should take an array of sort criteria, where each criterion specifies the key to sort by and the direction (ascending or descending).

## Solution

We can use the `sort` method with a custom comparison function. The comparison function will iterate through the sort criteria and compare the objects based on each criterion until a difference is found.

```javascript
function sortByMultipleFields(arr, criteria) {
  return arr.sort((a, b) => {
    for (const criterion of criteria) {
      const { key, direction = 'asc' } = criterion;
      const valA = a[key];
      const valB = b[key];

      const comparison = valA < valB ? -1 : (valA > valB ? 1 : 0);
      if (comparison !== 0) {
        return direction === 'asc' ? comparison : -comparison;
      }
    }
    return 0;
  });
}

// Example
const users = [
  { name: 'Alice', age: 30 },
  { name: 'Bob', age: 25 },
  { name: 'Alice', age: 25 }
];

const sortedUsers = sortByMultipleFields(users, [
  { key: 'name', direction: 'asc' },
  { key: 'age', direction: 'desc' }
]);

console.log(sortedUsers);
// [
//   { name: 'Alice', age: 30 },
//   { name: 'Alice', age: 25 },
//   { name: 'Bob', age: 25 }
// ]
```
