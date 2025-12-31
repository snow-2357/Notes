# Infinite Scroll Logic

## Problem

Implement the basic logic for infinite scrolling. When a user scrolls near the bottom of a container, more content should be triggered to load. This logic should be adaptable to different environments (e.g., browser, custom scrollable components).

## Solution

The core logic involves tracking the scroll position relative to the total scrollable height and a defined threshold. We also need to manage a loading state to prevent multiple data fetches for a single scroll event. This function usually works in conjunction with a debounced or throttled event listener.

```javascript
/**
 * Determines if a scroll event has reached the end threshold.
 * @param {object} scrollData - Object containing scroll information.
 * @param {number} scrollData.scrollTop - The current vertical scroll position.
 * @param {number} scrollData.scrollHeight - The total height of the scrollable content.
 * @param {number} scrollData.clientHeight - The visible height of the scrollable area.
 * @param {number} threshold - How close to the bottom (in pixels) before triggering.
 * @returns {boolean} - True if the scroll position is within the threshold of the bottom.
 */
function hasReachedBottom(scrollData, threshold) {
  const { scrollTop, scrollHeight, clientHeight } = scrollData;
  return scrollTop + clientHeight >= scrollHeight - threshold;
}

// --- Example usage with a mock API and state management ---

// Mock data fetching function
async function fetchItems(page, limit) {
  console.log(`Fetching items for page ${page} with limit ${limit}...`);
  return new Promise(resolve => {
    setTimeout(() => {
      const startId = (page - 1) * limit + 1;
      const newItems = Array.from({ length: limit }, (_, i) => ({ id: startId + i, name: `Item ${startId + i}` }));
      console.log(`Fetched ${newItems.length} items.`);
      resolve(newItems);
    }, 500); // Simulate network delay
  });
}

// Simple state management for the example
let currentPage = 1;
let allItems = [];
let isLoading = false;
const ITEMS_PER_PAGE = 10;
const SCROLL_THRESHOLD = 200; // Pixels from bottom to trigger load

async function loadNextPage() {
  if (isLoading) return;
  isLoading = true;
  console.log("Loading more content...");

  try {
    const newItems = await fetchItems(currentPage, ITEMS_PER_PAGE);
    allItems = allItems.concat(newItems);
    currentPage++;
  } catch (error) {
    console.error("Failed to load more items:", error);
  } finally {
    isLoading = false;
  }
  console.log(`Total items: ${allItems.length}`);
}

// Simulate a scroll event. In a browser, this would come from `window.addEventListener('scroll', ...)`.
function simulateScroll(currentScrollTop, totalScrollHeight, visibleHeight) {
  const scrollData = {
    scrollTop: currentScrollTop,
    scrollHeight: totalScrollHeight,
    clientHeight: visibleHeight
  };

  if (hasReachedBottom(scrollData, SCROLL_THRESHOLD)) {
    console.log("Reached scroll threshold. Attempting to load next page.");
    loadNextPage();
  }
}

// Initial load
loadNextPage();

// Simulate some scrolling actions
// console.log("\n--- Simulating scroll 1 (not yet at bottom) ---");
// simulateScroll(100, 1000, 300); // scrollTop 100, scrollHeight 1000, clientHeight 300

// console.log("\n--- Simulating scroll 2 (at bottom) ---");
// simulateScroll(750, 1000, 300); // scrollTop 750, scrollHeight 1000, clientHeight 300
// (This will trigger loadNextPage)
```