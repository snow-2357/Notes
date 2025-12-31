# Group Object Values by Key

## Problem

This title is a bit ambiguous. It could mean grouping an array of objects by a key, or something else. Based on the "Objects" category, a likely interpretation is to group the values of a single object by some criteria. A more common task is to group an *array of objects* by a key, which is covered in the "Array of Objects" section.

Let's assume the goal is to invert an object, grouping keys by their value. For example, if you have an object mapping students to their grades, you might want to create an object mapping grades to the students who achieved them.

**Problem Statement (Re-interpreted):** Given an object, create a new object where the keys are the unique values from the original object, and the values are arrays of keys from the original object that had that value.

## Solution

```javascript
function groupKeysByValue(obj) {
  const grouped = {};
  for (const key in obj) {
    const value = obj[key];
    if (!grouped[value]) {
      grouped[value] = [];
    }
    grouped[value].push(key);
  }
  return grouped;
}

// Example
const studentGrades = {
  'Alice': 'A',
  'Bob': 'B',
  'Charlie': 'A',
  'David': 'C'
};

const gradesToStudents = groupKeysByValue(studentGrades);
console.log(gradesToStudents);
// {
//   'A': ['Alice', 'Charlie'],
//   'B': ['Bob'],
//   'C': ['David']
// }
```
