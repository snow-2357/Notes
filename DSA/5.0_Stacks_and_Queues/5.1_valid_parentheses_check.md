# Valid Parentheses Check

## Problem

Given a string containing just the characters `(`, `)`, `{`, `}`, `[` and `]`, determine if the input string is valid. An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

## Solution

We can use a stack to solve this problem. We iterate through the string. If we encounter an opening bracket, we push it onto the stack. If we encounter a closing bracket, we check if the stack is empty or if the top of the stack is the corresponding opening bracket. If not, the string is invalid. At the end, if the stack is empty, the string is valid.

```javascript
function isValidParentheses(s) {
  const stack = [];
  const map = {
    '(': ')',
    '{': '}',
    '[': ']'
  };

  for (let i = 0; i < s.length; i++) {
    const char = s[i];
    if (map[char]) {
      stack.push(char);
    } else {
      if (stack.length === 0) {
        return false;
      }
      const lastOpen = stack.pop();
      if (map[lastOpen] !== char) {
        return false;
      }
    }
  }

  return stack.length === 0;
}

// Example
console.log(isValidParentheses("()")); // true
console.log(isValidParentheses("()[]{}")); // true
console.log(isValidParentheses("(]")); // false
console.log(isValidParentheses("([)]")); // false
console.log(isValidParentheses("{[]}")); // true
```
