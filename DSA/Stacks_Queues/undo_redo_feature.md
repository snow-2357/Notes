# Undo/Redo Feature

## Problem

Implement an undo/redo feature for a text editor using two stacks.

## Solution

This is very similar to the browser history simulation. We can use an `undoStack` and a `redoStack`. When a change is made, we push the previous state onto the `undoStack` and clear the `redoStack`. To undo, we pop from the `undoStack` and push the current state onto the `redoStack`. To redo, we pop from the `redoStack` and push the current state onto the `undoStack`.

```javascript
class TextEditor {
  constructor() {
    this.text = '';
    this.undoStack = [];
    this.redoStack = [];
  }

  type(newText) {
    this.undoStack.push(this.text);
    this.text += newText;
    this.redoStack = []; // Clear redo history on new action
    console.log(`Current text: "${this.text}"`);
  }

  undo() {
    if (this.undoStack.length > 0) {
      this.redoStack.push(this.text);
      this.text = this.undoStack.pop();
      console.log(`Undo! Current text: "${this.text}"`);
    } else {
      console.log("Nothing to undo.");
    }
  }

  redo() {
    if (this.redoStack.length > 0) {
      this.undoStack.push(this.text);
      this.text = this.redoStack.pop();
      console.log(`Redo! Current text: "${this.text}"`);
    } else {
      console.log("Nothing to redo.");
    }
  }
}

// Example
const editor = new TextEditor();
editor.type('Hello');
editor.type(' World');
editor.undo();    // Undo! Current text: "Hello"
editor.redo();    // Redo! Current text: "Hello World"
editor.undo();    // Undo! Current text: "Hello"
editor.undo();    // Undo! Current text: ""
editor.undo();    // Nothing to undo
```
