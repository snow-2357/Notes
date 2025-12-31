# Paginate Array of Objects

## Problem

Given an array of objects, write a function that paginates the array. The function should take the array, a page number, and the number of items per page as input, and return the items for the specified page.

## Solution

We can use `slice` to extract the correct portion of the array.

```javascript
function paginate(arr, page, itemsPerPage) {
  const startIndex = (page - 1) * itemsPerPage;
  const endIndex = startIndex + itemsPerPage;
  return arr.slice(startIndex, endIndex);
}

// Example
const data = [
  { id: 1 }, { id: 2 }, { id: 3 }, { id: 4 }, { id: 5 },
  { id: 6 }, { id: 7 }, { id: 8 }, { id: 9 }, { id: 10 }
];

const page1 = paginate(data, 1, 3);
console.log(page1); // [{ id: 1 }, { id: 2 }, { id: 3 }]

const page3 = paginate(data, 3, 3);
console.log(page3); // [{ id: 7 }, { id: 8 }, { id: 9 }]
```
