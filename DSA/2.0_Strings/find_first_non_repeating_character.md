# Find First Non-Repeating Character

## Problem

Write a function that takes a string and finds the first character that does not repeat anywhere in the string.

## Solution

We can use a hash map to store the frequency of each character. We'll iterate through the string once to build the frequency map. Then, we'll iterate through the string again and return the first character with a frequency of 1.

```javascript
function findFirstNonRepeatingChar(str) {
  const frequency = {};
  for (const char of str) {
    frequency[char] = (frequency[char] || 0) + 1;
  }

  for (const char of str) {
    if (frequency[char] === 1) {
      return char;
    }
  }

  return null; // or undefined, if no non-repeating character is found
}

// Example
console.log(findFirstNonRepeatingChar('swiss')); // 'w'
console.log(findFirstNonRepeatingChar('programming')); // 'p'
console.log(findFirstNonRepeatingChar('aabbcc')); // null
```
