# Implement Stack Using Array

## Problem

Implement a Stack data structure using an array. A stack is a Last-In-First-Out (LIFO) data structure. It should have the following methods:
- `push(item)`: Adds an item to the top of the stack.
- `pop()`: Removes an item from the top of the stack.
- `peek()`: Returns the item at the top of the stack without removing it.
- `isEmpty()`: Returns `true` if the stack is empty, `false` otherwise.
- `size()`: Returns the number of items in the stack.

## Solution

We can use an array to store the stack's elements. For `push`, we'll use the array's `push` method. For `pop`, we'll use the array's `pop` method.

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(item) {
    this.items.push(item);
  }

  pop() {
    if (this.isEmpty()) {
      return "Underflow";
    }
    return this.items.pop();
  }

  peek() {
    return this.isEmpty() ? undefined : this.items[this.items.length - 1];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }
}

// Example
const stack = new Stack();
stack.push(10);
stack.push(20);
stack.push(30);

console.log(stack.pop());  // 30
console.log(stack.peek()); // 20
console.log(stack.size()); // 2
```
