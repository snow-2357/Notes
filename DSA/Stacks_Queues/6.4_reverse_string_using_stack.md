# Reverse String Using Stack

## Problem

Write a function that reverses a string using a stack.

## Solution

We can push all characters of the string onto a stack. Then, we can pop the characters from the stack one by one to build the reversed string.

```javascript
function reverseStringWithStack(str) {
  const stack = [];
  for (const char of str) {
    stack.push(char);
  }

  let reversedStr = '';
  while (stack.length > 0) {
    reversedStr += stack.pop();
  }

  return reversedStr;
}

// Example
const text = 'hello world';
const reversedText = reverseStringWithStack(text);
console.log(reversedText); // 'dlrow olleh'
```
