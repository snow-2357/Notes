# Sum Values by Category

## Problem

Given an array of objects, where each object has a category and a value, calculate the sum of values for each category.

## Solution

We can use `reduce` to iterate over the array and build an object that stores the sum for each category.

```javascript
function sumByCategory(arr, categoryKey, valueKey) {
  return arr.reduce((acc, obj) => {
    const category = obj[categoryKey];
    const value = obj[valueKey];

    if (!acc[category]) {
      acc[category] = 0;
    }
    acc[category] += value;

    return acc;
  }, {});
}

// Example
const expenses = [
  { category: 'Groceries', amount: 50 },
  { category: 'Transportation', amount: 30 },
  { category: 'Groceries', amount: 70 },
  { category: 'Entertainment', amount: 40 },
  { category: 'Transportation', amount: 20 }
];

const totalByCategory = sumByCategory(expenses, 'category', 'amount');
console.log(totalByCategory);
// {
//   Groceries: 120,
//   Transportation: 50,
//   Entertainment: 40
// }
```
