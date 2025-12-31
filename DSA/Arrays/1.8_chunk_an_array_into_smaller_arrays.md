# Chunk an Array into Smaller Arrays

## Problem

Given an array and a chunk size, divide the array into many subarrays where each subarray is of length size.

## Solution

We can iterate through the array and use `slice()` to create chunks of the desired size.

```javascript
function chunkArray(arr, size) {
  const chunked = [];
  for (let i = 0; i < arr.length; i += size) {
    chunked.push(arr.slice(i, i + size));
  }
  return chunked;
}

// Example
const array = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const chunkedArray = chunkArray(array, 3);
console.log(chunkedArray); // [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```
