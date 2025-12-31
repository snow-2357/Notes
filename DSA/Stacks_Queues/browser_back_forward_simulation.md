# Browser Back/Forward Simulation

## Problem

Implement a browser history simulation using two stacks. You should be able to visit a new URL, go back to the previous URL, and go forward to the next URL.

## Solution

We can use two stacks: one for the back history and one for the forward history. When we visit a new URL, we push the current URL onto the back stack and clear the forward stack. When we go back, we pop from the back stack and push the current URL onto the forward stack. When we go forward, we pop from the forward stack and push the current URL onto the back stack.

```javascript
class BrowserHistory {
  constructor(homepage) {
    this.backStack = [];
    this.forwardStack = [];
    this.currentPage = homepage;
  }

  visit(url) {
    this.backStack.push(this.currentPage);
    this.currentPage = url;
    this.forwardStack = []; // Clear forward history on new visit
    console.log(`Visited: ${this.currentPage}`);
  }

  back() {
    if (this.backStack.length > 0) {
      this.forwardStack.push(this.currentPage);
      this.currentPage = this.backStack.pop();
      console.log(`Back to: ${this.currentPage}`);
      return this.currentPage;
    }
    console.log("No back history.");
    return null;
  }

  forward() {
    if (this.forwardStack.length > 0) {
      this.backStack.push(this.currentPage);
      this.currentPage = this.forwardStack.pop();
      console.log(`Forward to: ${this.currentPage}`);
      return this.currentPage;
    }
    console.log("No forward history.");
    return null;
  }
}

// Example
const browser = new BrowserHistory('homepage.com');
browser.visit('page1.com');
browser.visit('page2.com');
browser.back();      // Back to: page1.com
browser.back();      // Back to: homepage.com
browser.forward();   // Forward to: page1.com
browser.visit('page3.com');
browser.forward();   // No forward history.
```
