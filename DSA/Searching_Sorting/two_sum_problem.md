# Two Sum Problem

## Problem

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`. You may assume that each input would have exactly one solution, and you may not use the same element twice.

## Solution

We can use a hash map (object in JavaScript) to store numbers as we iterate through the array. For each number, we calculate the `complement` (target - current number). If the complement exists in our hash map, we've found our pair.

```javascript
function twoSum(nums, target) {
  const numMap = {}; // value -> index

  for (let i = 0; i < nums.length; i++) {
    const currentNum = nums[i];
    const complement = target - currentNum;

    if (complement in numMap) {
      return [numMap[complement], i];
    }
    numMap[currentNum] = i;
  }
  return []; // Should not reach here given the problem statement
}

// Example
console.log(twoSum([2, 7, 11, 15], 9)); // [0, 1] (because nums[0] + nums[1] == 9)
console.log(twoSum([3, 2, 4], 6));      // [1, 2]
console.log(twoSum([3, 3], 6));          // [0, 1]
```
