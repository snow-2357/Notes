# Form Validation Logic

## Problem

Implement a flexible form validation logic that can handle various validation rules (e.g., required, minLength, maxLength, email format, custom regex) for multiple input fields.

## Solution

We can define validation rules for each field and then create a validation function that iterates through the fields and applies their respective rules.

```javascript
const validationRules = {
  name: {
    required: true,
    minLength: 3,
    maxLength: 50
  },
  email: {
    required: true,
    pattern: /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  },
  password: {
    required: true,
    minLength: 6
  }
};

function validateForm(formData, rules) {
  const errors = {};

  for (const fieldName in rules) {
    const fieldRules = rules[fieldName];
    const value = formData[fieldName];

    if (fieldRules.required && (value === undefined || value === null || value.trim() === '')) {
      errors[fieldName] = `${fieldName} is required.`;
      continue;
    }

    if (fieldRules.minLength && value && value.length < fieldRules.minLength) {
      errors[fieldName] = `${fieldName} must be at least ${fieldRules.minLength} characters long.`;
      continue;
    }

    if (fieldRules.maxLength && value && value.length > fieldRules.maxLength) {
      errors[fieldName] = `${fieldName} must be no more than ${fieldRules.maxLength} characters long.`;
      continue;
    }

    if (fieldRules.pattern && value && !fieldRules.pattern.test(value)) {
      errors[fieldName] = `${fieldName} is not in a valid format.`;
      continue;
    }
  }

  return errors;
}

// Example
const user1 = {
  name: 'John Doe',
  email: 'john.doe@example.com',
  password: 'password123'
};

const user2 = {
  name: 'Jo', // Too short
  email: 'invalid-email', // Invalid format
  password: '' // Required
};

console.log('Validation for User 1:', validateForm(user1, validationRules)); // {} (no errors)
console.log('Validation for User 2:', validateForm(user2, validationRules));
// {
//   name: 'name must be at least 3 characters long.',
//   email: 'email is not in a valid format.',
//   password: 'password is required.'
// }
```
