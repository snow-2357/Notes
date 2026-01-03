# Min Stack Implementation

## Problem

Design a stack that supports `push`, `pop`, `peek`, and `getMin` in constant time. `getMin` should retrieve the minimum element in the stack.

## Solution

We can use two stacks. One stack will be the main stack, and the other stack (the min-stack) will keep track of the minimum element at each level of the main stack.

```javascript
class MinStack {
  constructor() {
    this.stack = [];
    this.minStack = [];
  }

  push(item) {
    this.stack.push(item);
    if (this.minStack.length === 0 || item <= this.getMin()) {
      this.minStack.push(item);
    }
  }

  pop() {
    if (this.isEmpty()) {
      return "Underflow";
    }
    const popped = this.stack.pop();
    if (popped === this.getMin()) {
      this.minStack.pop();
    }
    return popped;
  }

  peek() {
    return this.isEmpty() ? undefined : this.stack[this.stack.length - 1];
  }

  getMin() {
    return this.minStack.length === 0 ? undefined : this.minStack[this.minStack.length - 1];
  }

  isEmpty() {
    return this.stack.length === 0;
  }
}

// Example
const minStack = new MinStack();
minStack.push(5);
minStack.push(2);
minStack.push(7);
minStack.push(1);

console.log(minStack.getMin()); // 1
minStack.pop();
console.log(minStack.getMin()); // 2
```
