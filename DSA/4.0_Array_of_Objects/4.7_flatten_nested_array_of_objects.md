# Flatten Nested Array of Objects

## Problem

Given an array of objects that may contain a nested array of objects under a specific key, flatten the structure. Each object in the nested array should be brought to the top level, merged with its parent object.

## Solution

We can use `reduce` to iterate through the array. For each object, we check if it has the nested array. If it does, we map over the nested array to create new flattened objects. If not, we just keep the object as is.

```javascript
function flattenNestedArrayOfObjects(arr, nestedKey) {
  return arr.reduce((acc, obj) => {
    if (obj[nestedKey] && Array.isArray(obj[nestedKey])) {
      const children = obj[nestedKey].map(child => ({ ...obj, ...child }));
      delete children[nestedKey]; // remove the nested array from the new objects
      return acc.concat(children);
    }
    return acc.concat(obj);
  }, []);
}

// Example
const data = [
  {
    id: 1,
    name: 'Category A',
    items: [
      { itemId: 101, itemName: 'Item 1' },
      { itemId: 102, itemName: 'Item 2' }
    ]
  },
  {
    id: 2,
    name: 'Category B'
  }
];

const flattenedData = flattenNestedArrayOfObjects(data, 'items');
console.log(flattenedData);
// [
//   { id: 1, name: 'Category A', itemId: 101, itemName: 'Item 1' },
//   { id: 1, name: 'Category A', itemId: 102, itemName: 'Item 2' },
//   { id: 2, name: 'Category B' }
// ]
```
