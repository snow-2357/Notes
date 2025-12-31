# Anagram Check

## Problem

Given two strings, write a function to determine if the second string is an anagram of the first. An anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Solution

A simple solution is to clean and sort both strings and then compare them.

```javascript
function isAnagram(str1, str2) {
  const cleanStr1 = str1.replace(/[^a-zA-Z0-9]/g, '').toLowerCase();
  const cleanStr2 = str2.replace(/[^a-zA-Z0-9]/g, '').toLowerCase();

  if (cleanStr1.length !== cleanStr2.length) {
    return false;
  }

  const sortedStr1 = cleanStr1.split('').sort().join('');
  const sortedStr2 = cleanStr2.split('').sort().join('');

  return sortedStr1 === sortedStr2;
}

// Example
console.log(isAnagram('rail safety', 'fairy tales')); // true
console.log(isAnagram('hello', 'world')); // false
```

### Using a Frequency Counter

A more performant solution for longer strings is to use a frequency counter (a hash map or object) to count the characters in each string.

```javascript
function isAnagramWithFrequencyCounter(str1, str2) {
    const cleanStr1 = str1.replace(/[^a-zA-Z0-9]/g, '').toLowerCase();
    const cleanStr2 = str2.replace(/[^a-zA-Z0-9]/g, '').toLowerCase();

    if (cleanStr1.length !== cleanStr2.length) {
        return false;
    }

    const frequency = {};

    for (const char of cleanStr1) {
        frequency[char] = (frequency[char] || 0) + 1;
    }

    for (const char of cleanStr2) {
        if (!frequency[char]) {
            return false;
        }
        frequency[char]--;
    }

    return true;
}

// Example
console.log(isAnagramWithFrequencyCounter('rail safety', 'fairy tales')); // true
console.log(isAnagramWithFrequencyCounter('hello', 'world')); // false
```
