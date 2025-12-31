# Rate Limiter Function

## Problem

Implement a rate limiter function that restricts a function from being called more than a certain number of times within a specified time window.

## Solution (Token Bucket Algorithm)

A common approach for rate limiting is the Token Bucket algorithm. Imagine a bucket that holds a fixed number of "tokens". Tokens are added to the bucket at a fixed rate. Each time an operation is performed, one token is removed from the bucket. If the bucket is empty, the operation is delayed or rejected.

```javascript
function createRateLimiter(limit, interval) {
  let tokens = limit;
  let lastRefillTime = Date.now();
  let queue = []; // Queue for deferred function calls

  function refillTokens() {
    const now = Date.now();
    const timePassed = now - lastRefillTime;
    const tokensToAdd = Math.floor(timePassed / interval) * limit; // Refill all tokens for each interval passed
    tokens = Math.min(limit, tokens + tokensToAdd);
    lastRefillTime = now;
  }

  return function(func, ...args) {
    refillTokens(); // Always refill before attempting to use

    if (tokens > 0) {
      tokens--;
      func(...args);
    } else {
      // Option 1: Reject immediately
      // console.log("Rate limit exceeded. Function call rejected.");

      // Option 2: Queue the function call (more complex, but can be useful)
      console.log("Rate limit exceeded. Function call queued.");
      queue.push({ func, args });

      // Process queue after some time, or implement a separate scheduler
      if (!createRateLimiter.queueProcessor) {
        createRateLimiter.queueProcessor = setInterval(() => {
          if (queue.length > 0) {
            refillTokens();
            while (tokens > 0 && queue.length > 0) {
              tokens--;
              const { func, args } = queue.shift();
              func(...args);
            }
          }
        }, interval / limit); // Check more frequently
      }
    }
  };
}

// Example
const logger = (message) => console.log(`${Date.now() % 10000}: ${message}`);
const rateLimitedLogger = createRateLimiter(2, 1000); // Allow 2 calls per second

rateLimitedLogger(logger, 'Call 1'); // Should execute immediately
rateLimitedLogger(logger, 'Call 2'); // Should execute immediately
rateLimitedLogger(logger, 'Call 3'); // Should be queued
rateLimitedLogger(logger, 'Call 4'); // Should be queued

setTimeout(() => {
  rateLimitedLogger(logger, 'Call 5'); // Should execute after refill
}, 1100);

setTimeout(() => {
  rateLimitedLogger(logger, 'Call 6'); // Should execute after refill
}, 1200);

// Clear the interval if using queue processor
// setTimeout(() => {
//   clearInterval(createRateLimiter.queueProcessor);
// }, 5000);
```

This is a more sophisticated rate limiter. For simpler cases, a basic throttling mechanism might suffice (see `implement_throttle.md`).
