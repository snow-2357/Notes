# Tree Traversal (DFS) using Recursion

## Problem

Given a tree-like data structure (like a binary tree or a nested object representing a file system), perform a Depth-First Search (DFS) traversal and print the values of each node.

## Solution

We can use recursion to implement DFS. For a given node, we first process its value, then we recursively call the traversal function for each of its children.

Let's use a simple binary tree as an example.

```javascript
// Definition for a binary tree node.
class TreeNode {
  constructor(val, left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

// Pre-order traversal (Root, Left, Right)
function dfsPreOrder(node) {
  if (node === null) {
    return;
  }
  console.log(node.val);
  dfsPreOrder(node.left);
  dfsPreOrder(node.right);
}

// In-order traversal (Left, Root, Right)
function dfsInOrder(node) {
    if (node === null) {
        return;
    }
    dfsInOrder(node.left);
    console.log(node.val);
    dfsInOrder(node.right);
}

// Post-order traversal (Left, Right, Root)
function dfsPostOrder(node) {
    if (node === null) {
        return;
    }
    dfsPostOrder(node.left);
    dfsPostOrder(node.right);
    console.log(node.val);
}


// Example
const root = new TreeNode(1,
  new TreeNode(2, new TreeNode(4), new TreeNode(5)),
  new TreeNode(3)
);

console.log("Pre-order:");
dfsPreOrder(root); // 1, 2, 4, 5, 3

console.log("\\nIn-order:");
dfsInOrder(root); // 4, 2, 5, 1, 3

console.log("\\nPost-order:");
dfsPostOrder(root); // 4, 5, 2, 3, 1
```
