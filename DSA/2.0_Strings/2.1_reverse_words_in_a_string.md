# Reverse Words in a String

## Problem

Given a string, write a function that reverses the order of the words in the string.

## Solution

A straightforward approach is to split the string into an array of words, reverse the array, and then join the words back into a string.

```javascript
function reverseWords(str) {
  return str.split(' ').reverse().join(' ');
}

// Example
const sentence = 'hello world from javascript';
const reversedSentence = reverseWords(sentence);
console.log(reversedSentence); // 'javascript from world hello'
```
