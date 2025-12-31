# Find Kth Largest Element

## Problem

Given an unsorted array of numbers, find the k-th largest element in the array. Note that it is the k-th largest element in the sorted order, not the k-th distinct element.

## Solution

A straightforward solution is to sort the array and then pick the k-th element from the end.

```javascript
function findKthLargest(arr, k) {
  arr.sort((a, b) => a - b); // Sort in ascending order
  return arr[arr.length - k];
}

// Example
const numbers = [3, 2, 1, 5, 6, 4];
console.log(findKthLargest(numbers, 2)); // 5 (The 2nd largest element)

const numbers2 = [3, 2, 3, 1, 2, 4, 5, 5, 6];
console.log(findKthLargest(numbers2, 4)); // 4 (The 4th largest element)
```

### Using a Min-Heap (Priority Queue)

For larger arrays or when `k` is relatively small, a min-heap (priority queue) can be more efficient than sorting the entire array.

```javascript
class MinHeap {
    constructor() {
        this.heap = [];
    }

    getParentIndex(i) { return Math.floor((i - 1) / 2); }
    getLeftChildIndex(i) { return 2 * i + 1; }
    getRightChildIndex(i) { return 2 * i + 2; }

    hasParent(i) { return this.getParentIndex(i) >= 0; }
    hasLeftChild(i) { return this.getLeftChildIndex(i) < this.heap.length; }
    hasRightChild(i) { return this.getRightChildIndex(i) < this.heap.length; }

    getParent(i) { return this.heap[this.getParentIndex(i)]; }
    getLeftChild(i) { return this.heap[this.getLeftChildIndex(i)]; }
    getRightChild(i) { return this.heap[this.getRightChildIndex(i)]; }

    peek() {
        if (this.heap.length === 0) return null;
        return this.heap[0];
    }

    insert(item) {
        this.heap.push(item);
        this.heapifyUp();
    }

    extractMin() {
        if (this.heap.length === 0) return null;
        if (this.heap.length === 1) return this.heap.pop();

        const item = this.heap[0];
        this.heap[0] = this.heap.pop();
        this.heapifyDown();
        return item;
    }

    heapifyUp() {
        let index = this.heap.length - 1;
        while (this.hasParent(index) && this.getParent(index) > this.heap[index]) {
            [this.heap[this.getParentIndex(index)], this.heap[index]] = [this.heap[index], this.heap[this.getParentIndex(index)]];
            index = this.getParentIndex(index);
        }
    }

    heapifyDown() {
        let index = 0;
        while (this.hasLeftChild(index)) {
            let smallerChildIndex = this.getLeftChildIndex(index);
            if (this.hasRightChild(index) && this.getRightChild(index) < this.getLeftChild(index)) {
                smallerChildIndex = this.getRightChildIndex(index);
            }

            if (this.heap[index] < this.heap[smallerChildIndex]) {
                break;
            } else {
                [this.heap[index], this.heap[smallerChildIndex]] = [this.heap[smallerChildIndex], this.heap[index]];
            }
            index = smallerChildIndex;
        }
    }

    size() {
        return this.heap.length;
    }
}

function findKthLargestWithHeap(arr, k) {
    const minHeap = new MinHeap();

    for (const num of arr) {
        minHeap.insert(num);
        if (minHeap.size() > k) {
            minHeap.extractMin();
        }
    }

    return minHeap.peek();
}

// Example
const numbers3 = [3, 2, 1, 5, 6, 4];
console.log(findKthLargestWithHeap(numbers3, 2)); // 5
```
