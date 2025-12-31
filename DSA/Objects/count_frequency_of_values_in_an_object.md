# Count Frequency of Values in an Object

## Problem

Given an object, write a function to count the frequency of each value in the object.

## Solution

We can iterate through the values of the object and use another object to store the frequency of each value.

```javascript
function countValueFrequency(obj) {
  const frequency = {};
  for (const value of Object.values(obj)) {
    frequency[value] = (frequency[value] || 0) + 1;
  }
  return frequency;
}

// Example
const data = { a: 'apple', b: 'banana', c: 'apple', d: 'orange', e: 'banana', f: 'apple' };
const frequency = countValueFrequency(data);
console.log(frequency); // { apple: 3, banana: 2, orange: 1 }
```
