# Build Autocomplete Search Logic

## Problem

Implement a basic autocomplete search feature. Given a list of words (or a dictionary) and a search query, suggest words that start with the query.

## Solution

A simple approach is to filter the dictionary based on whether each word starts with the given query (case-insensitively).

```javascript
function autocompleteSearch(dictionary, query) {
  if (!query) {
    return [];
  }
  const lowerCaseQuery = query.toLowerCase();
  return dictionary.filter(word =>
    word.toLowerCase().startsWith(lowerCaseQuery)
  );
}

// Example
const dictionary = [
  'apple', 'apricot', 'banana', 'band', 'cat', 'car', 'api'
];

console.log(autocompleteSearch(dictionary, 'ap')); // ['apple', 'apricot']
console.log(autocompleteSearch(dictionary, 'ban')); // ['banana', 'band']
console.log(autocompleteSearch(dictionary, 'a')); // ['apple', 'apricot', 'api']
console.log(autocompleteSearch(dictionary, 'xyz')); // []
```

### More Advanced (Trie Data Structure)

For larger datasets and more efficient prefix searching, a Trie (prefix tree) data structure is typically used.

```javascript
class TrieNode {
  constructor() {
    this.children = {};
    this.isEndOfWord = false;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(word) {
    let current = this.root;
    for (const char of word) {
      if (!current.children[char]) {
        current.children[char] = new TrieNode();
      }
      current = current.children[char];
    }
    current.isEndOfWord = true;
  }

  search(prefix) {
    let current = this.root;
    for (const char of prefix) {
      if (!current.children[char]) {
        return []; // No words with this prefix
      }
      current = current.children[char];
    }

    const suggestions = [];
    this._collectWords(current, prefix, suggestions);
    return suggestions;
  }

  _collectWords(node, currentPrefix, suggestions) {
    if (node.isEndOfWord) {
      suggestions.push(currentPrefix);
    }
    for (const char in node.children) {
      this._collectWords(node.children[char], currentPrefix + char, suggestions);
    }
  }
}

// Example with Trie
const trie = new Trie();
const dictionaryTrie = ['apple', 'apricot', 'banana', 'band', 'cat', 'car', 'api'];
dictionaryTrie.forEach(word => trie.insert(word));

console.log(trie.search('ap')); // ['apple', 'apricot']
console.log(trie.search('ban')); // ['banana', 'band']
```
