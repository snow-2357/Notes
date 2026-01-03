# Capitalize First Letter of Each Word

## Problem

Write a function that accepts a string and capitalizes the first letter of each word in the string.

## Solution

We can split the string into an array of words, then iterate over the array, capitalizing the first letter of each word. Finally, we join the words back into a string.

```javascript
function capitalizeWords(str) {
  return str.split(' ').map(word => {
    return word.charAt(0).toUpperCase() + word.slice(1);
  }).join(' ');
}

// Example
const sentence = 'hello world from javascript';
const capitalizedSentence = capitalizeWords(sentence);
console.log(capitalizedSentence); // 'Hello World From Javascript'
```
