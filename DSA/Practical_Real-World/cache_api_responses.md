# Cache API Responses

## Problem

Implement a caching mechanism for API responses to improve performance and reduce redundant network requests. The cache should store responses for a certain duration (TTL - Time To Live).

## Solution

We can use an in-memory object (Map or simple object) to store cached responses. Each cache entry will include the response data and a timestamp indicating when it was cached. When a request comes in, we first check the cache. If a valid, non-expired response is found, we return it. Otherwise, we make the API call, store its response in the cache, and then return it.

```javascript
const apiCache = new Map(); // Stores { data: ..., timestamp: ... }

async function cachedFetch(url, options = {}, ttl = 60000) { // Default TTL: 60 seconds
  const cacheKey = JSON.stringify({ url, options });
  const cached = apiCache.get(cacheKey);

  if (cached && (Date.now() - cached.timestamp < ttl)) {
    console.log(`Returning cached response for ${url}`);
    return cached.data;
  }

  console.log(`Fetching fresh data for ${url}`);
  try {
    const response = await fetch(url, options);
    const data = await response.json(); // Assuming JSON response
    apiCache.set(cacheKey, { data, timestamp: Date.now() });
    return data;
  } catch (error) {
    console.error(`Error fetching ${url}:`, error);
    throw error;
  }
}

// Example usage (assuming fetch is available, e.g., in browser or node-fetch)
// To run this example in Node.js, you might need to install 'node-fetch'
// npm install node-fetch
// const fetch = require('node-fetch');

async function runExample() {
  // First call, fetches data
  await cachedFetch('https://jsonplaceholder.typicode.com/todos/1');

  // Second call within TTL, returns cached data
  await cachedFetch('https://jsonplaceholder.typicode.com/todos/1');

  // Wait for cache to expire (e.g., set TTL to 100ms for testing)
  // then fetch again
  await new Promise(resolve => setTimeout(resolve, 60000)); // wait for default 60s TTL
  await cachedFetch('https://jsonplaceholder.typicode.com/todos/1'); // Fetches again
}

// runExample(); // Uncomment to run the example
```
