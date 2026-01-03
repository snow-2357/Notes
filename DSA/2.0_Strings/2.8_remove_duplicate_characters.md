# Remove Duplicate Characters

## Problem

Write a function that removes duplicate characters from a string. The function should return a new string with all duplicate characters removed. The order of the characters should be preserved.

## Solution

We can use a `Set` to keep track of the characters we've already added to our result. A `Set` only stores unique values, which makes it perfect for this task.

```javascript
function removeDuplicateCharacters(str) {
  const charSet = new Set(str.split(''));
  return [...charSet].join('');
}

// Example
const text = 'hello world';
const uniqueText = removeDuplicateCharacters(text);
console.log(uniqueText); // 'helo wrd'
```

If you need to preserve the order of the first occurrence:
```javascript
function removeDuplicateCharactersOrdered(str) {
  let result = '';
  const seen = new Set();
  for (const char of str) {
    if (!seen.has(char)) {
      seen.add(char);
      result += char;
    }
  }
  return result;
}

// Example
const text2 = 'programming is fun';
const uniqueText2 = removeDuplicateCharactersOrdered(text2);
console.log(uniqueText2); // 'progamin sfu'
```
