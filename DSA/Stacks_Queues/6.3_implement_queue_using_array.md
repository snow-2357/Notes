# Implement Queue Using Array

## Problem

Implement a Queue data structure using an array. A queue is a First-In-First-Out (FIFO) data structure. It should have the following methods:
- `enqueue(item)`: Adds an item to the end of the queue.
- `dequeue()`: Removes an item from the front of the queue.
- `peek()`: Returns the item at the front of the queue without removing it.
- `isEmpty()`: Returns `true` if the queue is empty, `false` otherwise.
- `size()`: Returns the number of items in the queue.

## Solution

We can use an array to store the queue's elements. For `enqueue`, we'll use `push`. For `dequeue`, we'll use `shift` to remove the first element.

```javascript
class Queue {
  constructor() {
    this.items = [];
  }

  enqueue(item) {
    this.items.push(item);
  }

  dequeue() {
    if (this.isEmpty()) {
      return "Underflow";
    }
    return this.items.shift();
  }

  peek() {
    return this.isEmpty() ? undefined : this.items[0];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }
}

// Example
const queue = new Queue();
queue.enqueue(10);
queue.enqueue(20);
queue.enqueue(30);

console.log(queue.dequeue()); // 10
console.log(queue.peek());    // 20
console.log(queue.size());    // 2
```
*Note: Using `shift()` on a large array can be inefficient because it requires re-indexing all subsequent elements. For performance-critical applications, a linked list or a circular buffer is a better choice for implementing a queue.*
