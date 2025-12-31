# Feature Flag Evaluation

## Problem

Implement a basic feature flag system. A feature flag allows you to enable or disable features in your application without deploying new code. The system should be able to check if a feature is enabled for a given user or context.

## Solution

We can store feature flag configurations in an object or map. Each flag can have rules, such as being enabled for certain user IDs, roles, or a percentage of users.

```javascript
const featureFlags = {
  'new-checkout-flow': {
    enabled: true,
    users: ['user123', 'user456'],
    percentage: 50 // 50% of users see this feature
  },
  'dark-mode-beta': {
    enabled: false,
    roles: ['admin']
  },
  'experimental-feature': {
    enabled: true
  }
};

function isFeatureEnabled(featureName, userContext = {}) {
  const flag = featureFlags[featureName];

  if (!flag || !flag.enabled) {
    return false;
  }

  // Check user specific rules
  if (flag.users && userContext.userId) {
    if (flag.users.includes(userContext.userId)) {
      return true;
    }
  }

  // Check role specific rules
  if (flag.roles && userContext.role) {
    if (flag.roles.includes(userContext.role)) {
      return true;
    }
  }

  // Check percentage rollout
  if (flag.percentage !== undefined) {
    // A simple way to simulate percentage rollout based on user ID or a random number
    // For a real-world scenario, you'd want a more deterministic approach (e.g., hash user ID)
    const randomValue = Math.random() * 100; // 0-99.99
    return randomValue < flag.percentage;
  }

  return flag.enabled; // Default to the general enabled status
}

// Example
console.log('New Checkout Flow for user123:', isFeatureEnabled('new-checkout-flow', { userId: 'user123' })); // true
console.log('New Checkout Flow for user789:', isFeatureEnabled('new-checkout-flow', { userId: 'user789' })); // Varies based on percentage
console.log('Dark Mode Beta for admin:', isFeatureEnabled('dark-mode-beta', { role: 'admin' })); // true
console.log('Experimental Feature:', isFeatureEnabled('experimental-feature')); // true
console.log('Non-existent Feature:', isFeatureEnabled('non-existent-feature')); // false
```
