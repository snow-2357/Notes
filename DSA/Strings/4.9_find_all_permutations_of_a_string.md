# Find All Permutations of a String

## Problem

Write a function that returns an array of all permutations of a given string.

## Solution

We can solve this using recursion. The base case is when the string has only one character, in which case the only permutation is the string itself. For longer strings, we can iterate through each character, and for each character, find all permutations of the rest of the string.

```javascript
function findAllPermutations(str) {
  if (str.length === 1) {
    return [str];
  }

  const permutations = [];
  for (let i = 0; i < str.length; i++) {
    const char = str[i];
    const remainingChars = str.slice(0, i) + str.slice(i + 1);
    const innerPermutations = findAllPermutations(remainingChars);
    for (const permutation of innerPermutations) {
      permutations.push(char + permutation);
    }
  }
  return permutations;
}

// Example
const perms = findAllPermutations('abc');
console.log(perms); // ['abc', 'acb', 'bac', 'bca', 'cab', 'cba']
```
