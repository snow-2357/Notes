# Filter Objects Based on Dynamic Conditions

## Problem

Write a function that filters an array of objects based on a dynamic set of conditions. The conditions are provided as an object where keys are the object properties to filter by, and values are the desired values.

## Solution

We can use `filter` on the array and for each object, check if it meets all the conditions specified in the filters object.

```javascript
function dynamicFilter(arr, filters) {
  return arr.filter(obj => {
    return Object.keys(filters).every(key => {
      return obj[key] === filters[key];
    });
  });
}

// Example
const products = [
  { name: 'Laptop', category: 'Electronics', price: 1200, inStock: true },
  { name: 'Shirt', category: 'Apparel', price: 25, inStock: true },
  { name: 'Coffee Maker', category: 'Appliances', price: 50, inStock: false },
  { name: 'T-Shirt', category: 'Apparel', price: 15, inStock: true }
];

const apparelInStock = dynamicFilter(products, { category: 'Apparel', inStock: true });
console.log(apparelInStock);
// [
//   { name: 'Shirt', category: 'Apparel', price: 25, inStock: true },
//   { name: 'T-Shirt', category: 'Apparel', price: 15, inStock: true }
// ]
```
