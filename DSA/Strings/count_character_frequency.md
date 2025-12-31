# Count Character Frequency

## Problem

Write a function that takes a string and returns an object where the keys are the characters in the string and the values are their frequencies.

## Solution

We can use a hash map (or a simple object in JavaScript) to store the frequency of each character. We iterate through the string, and for each character, we increment its count in the hash map.

```javascript
function countCharFrequency(str) {
  const frequency = {};
  for (const char of str) {
    frequency[char] = (frequency[char] || 0) + 1;
  }
  return frequency;
}

// Example
const text = 'hello world';
const frequency = countCharFrequency(text);
console.log(frequency);
// {
//   h: 1,
//   e: 1,
//   l: 3,
//   o: 2,
//   ' ': 1,
//   w: 1,
//   r: 1,
//   d: 1
// }
```
