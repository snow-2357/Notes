# Next Greater Element

## Problem

Given an array, find the next greater element for each element in the array. The next greater element for an element `x` is the first greater element on the right side of `x` in the array. If no such element exists, the next greater element is -1.

## Solution

We can use a stack to solve this problem efficiently. We iterate through the array from right to left. For each element, we pop elements from the stack that are smaller than or equal to the current element. The top of the stack is then the next greater element.

```javascript
function nextGreaterElement(arr) {
  const result = new Array(arr.length);
  const stack = [];

  for (let i = arr.length - 1; i >= 0; i--) {
    while (stack.length > 0 && stack[stack.length - 1] <= arr[i]) {
      stack.pop();
    }
    result[i] = stack.length === 0 ? -1 : stack[stack.length - 1];
    stack.push(arr[i]);
  }

  return result;
}

// Example
const arr = [4, 5, 2, 25];
const result = nextGreaterElement(arr);
console.log(result); // [5, 25, 25, -1]
```
