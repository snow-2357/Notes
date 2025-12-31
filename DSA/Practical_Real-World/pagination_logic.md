# Pagination Logic

## Problem

Implement pagination logic for displaying a large dataset in smaller, manageable chunks (pages). This involves calculating the total number of pages and returning the items for a specific page.

## Solution

The core of pagination involves knowing the total number of items and the number of items to display per page. From these, we can calculate the total number of pages and then use array `slice()` to get the items for the requested page.

```javascript
/**
 * Calculates pagination details and returns items for a specific page.
 * @param {Array} items - The full array of items to paginate.
 * @param {number} currentPage - The current page number (1-indexed).
 * @param {number} itemsPerPage - The number of items to display per page.
 * @returns {object} - An object containing currentPageItems, totalPages, and totalItems.
 */
function getPaginatedItems(items, currentPage, itemsPerPage) {
  const totalItems = items.length;
  const totalPages = Math.ceil(totalItems / itemsPerPage);

  const startIndex = (currentPage - 1) * itemsPerPage;
  const endIndex = startIndex + itemsPerPage;

  const currentPageItems = items.slice(startIndex, endIndex);

  return {
    currentPageItems,
    totalPages,
    totalItems,
    currentPage,
    itemsPerPage
  };
}

// Example
const allProducts = Array.from({ length: 100 }, (_, i) => ({ id: i + 1, name: `Product ${i + 1}` }));

// Get first page, 10 items per page
let pageData = getPaginatedItems(allProducts, 1, 10);
console.log('Page 1:', pageData.currentPageItems.map(p => p.name));
console.log('Total Pages:', pageData.totalPages); // 10

// Get fifth page, 10 items per page
pageData = getPaginatedItems(allProducts, 5, 10);
console.log('Page 5:', pageData.currentPageItems.map(p => p.name));

// Get last page
pageData = getPaginatedItems(allProducts, pageData.totalPages, 10);
console.log('Last Page:', pageData.currentPageItems.map(p => p.name));
```
