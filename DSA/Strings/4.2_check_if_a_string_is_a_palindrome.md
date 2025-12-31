# Check if a String is a Palindrome

## Problem

Given a string, write a function to check if it is a palindrome. A palindrome is a word, phrase, number, or other sequence of characters that reads the same backward as forward, disregarding punctuation, case, and spacing.

## Solution

A simple solution is to clean the string, reverse it, and then compare it to the original cleaned string.

```javascript
function isPalindrome(str) {
  const cleanStr = str.replace(/[^a-zA-Z0-9]/g, '').toLowerCase();
  const reversedStr = cleanStr.split('').reverse().join('');
  return cleanStr === reversedStr;
}

// Example
console.log(isPalindrome('A man, a plan, a canal: Panama')); // true
console.log(isPalindrome('hello world')); // false
```

### Two Pointer Approach

For a more optimized solution, we can use two pointers. One pointer starts at the beginning of the string, and the other starts at the end. We move the pointers towards the center, comparing characters along the way.

```javascript
function isPalindromeTwoPointers(str) {
    const cleanStr = str.replace(/[^a-zA-Z0-9]/g, '').toLowerCase();
    let left = 0;
    let right = cleanStr.length - 1;

    while (left < right) {
        if (cleanStr[left] !== cleanStr[right]) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

// Example
console.log(isPalindromeTwoPointers('A man, a plan, a canal: Panama')); // true
console.log(isPalindromeTwoPointers('hello world')); // false
```
