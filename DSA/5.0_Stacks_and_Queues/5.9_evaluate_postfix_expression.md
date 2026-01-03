# Evaluate Postfix Expression

## Problem

Write a function to evaluate a postfix expression (also known as Reverse Polish Notation). In postfix notation, the operators follow their operands.

## Solution

We can use a stack to solve this problem. We iterate through the expression. If we encounter a number, we push it onto the stack. If we encounter an operator, we pop the top two numbers from the stack, perform the operation, and push the result back onto the stack.

```javascript
function evaluatePostfix(expression) {
  const stack = [];
  const tokens = expression.split(' ');

  for (const token of tokens) {
    if (!isNaN(parseFloat(token))) {
      stack.push(parseFloat(token));
    } else {
      const operand2 = stack.pop();
      const operand1 = stack.pop();
      switch (token) {
        case '+':
          stack.push(operand1 + operand2);
          break;
        case '-':
          stack.push(operand1 - operand2);
          break;
        case '*':
          stack.push(operand1 * operand2);
          break;
        case '/':
          stack.push(operand1 / operand2);
          break;
        default:
          throw new Error(`Invalid operator: ${token}`);
      }
    }
  }

  return stack.pop();
}

// Example
const expression1 = "3 4 + 2 *"; // (3 + 4) * 2
console.log(evaluatePostfix(expression1)); // 14

const expression2 = "10 6 9 3 + -11 * / * 17 + 5 +";
console.log(evaluatePostfix(expression2)); // 22
```
