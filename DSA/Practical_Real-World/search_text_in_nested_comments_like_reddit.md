# Search Text in Nested Comments (like Reddit)

## Problem

Given a deeply nested structure of comments (like those found on Reddit or other forum sites), implement a function to search for a specific text string within the `content` of any comment, at any nesting level.

## Solution

We can use a recursive Depth-First Search (DFS) approach to traverse the nested comment structure. For each comment, we check its `content` for the search text. If the comment has `replies`, we recursively search through them.

```javascript
/**
 * Searches for text within a nested comment structure.
 * @param {Array<Object>} comments - An array of comment objects, each potentially having a 'replies' array.
 * @param {string} searchText - The text string to search for.
 * @returns {Array<Object>} - An array of comment objects that contain the search text.
 */
function searchComments(comments, searchText) {
  const matchingComments = [];
  const lowerSearchText = searchText.toLowerCase();

  function traverse(commentList) {
    for (const comment of commentList) {
      if (comment.content && comment.content.toLowerCase().includes(lowerSearchText)) {
        matchingComments.push(comment);
      }
      if (comment.replies && Array.isArray(comment.replies)) {
        traverse(comment.replies); // Recursive call for nested replies
      }
    }
  }

  traverse(comments);
  return matchingComments;
}

// Example
const nestedComments = [
  {
    id: 'c1',
    author: 'Alice',
    content: 'This is the main topic.',
    replies: [
      {
        id: 'c1-1',
        author: 'Bob',
        content: 'I agree with your point.',
        replies: [
          {
            id: 'c1-1-1',
            author: 'Charlie',
            content: 'That\'s an interesting perspective.',
            replies: []
          }
        ]
      },
      {
        id: 'c1-2',
        author: 'David',
        content: 'I have a different opinion.',
        replies: []
      }
    ]
  },
  {
    id: 'c2',
    author: 'Eve',
    content: 'Another unrelated comment.',
    replies: []
  }
];

console.log('Searching for "point":', searchComments(nestedComments, 'point'));
// [ { id: 'c1-1', author: 'Bob', content: 'I agree with your point.', replies: [...] } ]

console.log('Searching for "topic":', searchComments(nestedComments, 'topic'));
// [ { id: 'c1', author: 'Alice', content: 'This is the main topic.', replies: [...] } ]

console.log('Searching for "opinion":', searchComments(nestedComments, 'opinion'));
// [ { id: 'c1-2', author: 'David', content: 'I have a different opinion.', replies: [] } ]

console.log('Searching for "nonexistent":', searchComments(nestedComments, 'nonexistent')); // []
```
