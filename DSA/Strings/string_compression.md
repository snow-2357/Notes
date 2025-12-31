# String Compression

## Problem

Write a function to perform basic string compression using the counts of repeated characters. For example, the string "aabcccccaaa" would become "a2b1c5a3". If the "compressed" string would not become smaller than the original string, your function should return the original string.

## Solution

We can iterate through the string, keeping track of the current character and its count. When the character changes, we append the previous character and its count to the result.

```javascript
function compressString(str) {
  if (str.length === 0) {
    return "";
  }

  let compressed = '';
  let count = 1;

  for (let i = 0; i < str.length; i++) {
    if (str[i] === str[i + 1]) {
      count++;
    } else {
      compressed += str[i] + count;
      count = 1;
    }
  }

  return compressed.length < str.length ? compressed : str;
}

// Example
console.log(compressString('aabcccccaaa')); // 'a2b1c5a3'
console.log(compressString('abcdef')); // 'abcdef'
```
