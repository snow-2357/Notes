# Implement Stack Using Two Queues

## Problem

Implement a Stack data structure using two queues.

## Solution

We can implement a stack using two queues, `q1` and `q2`. The `push` operation is made costly.

**Push Operation (Costly):**
1. Enqueue the new element to `q2`.
2. Dequeue all elements from `q1` and enqueue them to `q2`.
3. Swap the names of `q1` and `q2`.

**Pop Operation:**
1. Dequeue from `q1`.

```javascript
class StackWithQueues {
  constructor() {
    this.q1 = []; // Use arrays as queues
    this.q2 = [];
  }

  push(item) {
    // Move all elements from q1 to q2
    while (this.q1.length > 0) {
      this.q2.push(this.q1.shift());
    }

    // Add the new item to q1
    this.q1.push(item);

    // Move all elements back to q1 from q2
    while (this.q2.length > 0) {
      this.q1.push(this.q2.shift());
    }
  }

  pop() {
    if (this.isEmpty()) {
      return "Underflow";
    }
    return this.q1.shift();
  }
  
  peek() {
    return this.isEmpty() ? undefined : this.q1[0];
  }

  isEmpty() {
    return this.q1.length === 0;
  }
}

// Example
const stack = new StackWithQueues();
stack.push(1);
stack.push(2);
stack.push(3);

console.log(stack.pop());  // 3
console.log(stack.peek()); // 2
```
This is just one way to do it. Another way is to make the `pop` operation costly.
