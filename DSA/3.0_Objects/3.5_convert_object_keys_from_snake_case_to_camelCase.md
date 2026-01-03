# Convert Object Keys from snake_case to camelCase

## Problem

Given an object with keys in snake_case, write a function to convert all the keys to camelCase. This should also work for nested objects.

## Solution

We can write a recursive function that traverses the object. For each key, we'll convert it to camelCase and then recursively call the function for any nested objects.

```javascript
function toCamelCase(str) {
  return str.replace(/([-_][a-z])/ig, ($1) => {
    return $1.toUpperCase()
      .replace('-', '')
      .replace('_', '');
  });
}

function keysToCamelCase(obj) {
  if (Array.isArray(obj)) {
    return obj.map(v => keysToCamelCase(v));
  } else if (obj !== null && obj.constructor === Object) {
    return Object.keys(obj).reduce((result, key) => {
      result[toCamelCase(key)] = keysToCamelCase(obj[key]);
      return result;
    }, {});
  }
  return obj;
}

// Example
const snakeCaseObject = {
  first_name: 'John',
  last_name: 'Doe',
  user_details: {
    phone_number: '123-456-7890'
  }
};

const camelCaseObject = keysToCamelCase(snakeCaseObject);
console.log(camelCaseObject);
// {
//   firstName: 'John',
//   lastName: 'Doe',
//   userDetails: {
//     phoneNumber: '123-456-7890'
//   }
// }
```
