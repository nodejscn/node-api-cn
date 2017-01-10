
The [`process.emitWarning()`][process_emit_warning] method can be used to issue
custom or application specific warnings.

```js
// Emit a warning using a string...
process.emitWarning('Something happened!');
  // Prints: (node 12345) Warning: Something happened!

// Emit a warning using an object...
process.emitWarning('Something Happened!', 'CustomWarning');
  // Prints: (node 12345) CustomWarning: Something happened!

// Emit a warning using a custom Error object...
class CustomWarning extends Error {
  constructor(message) {
    super(message);
    this.name = 'CustomWarning';
    Error.captureStackTrace(this, CustomWarning);
  }
}
const myWarning = new CustomWarning('Something happened!');
process.emitWarning(myWarning);
  // Prints: (node 12345) CustomWarning: Something happened!
```

