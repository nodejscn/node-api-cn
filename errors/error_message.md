
Returns the string description of error as set by calling `new Error(message)`.
The `message` passed to the constructor will also appear in the first line of
the stack trace of the `Error`, however changing this property after the
`Error` object is created *may not* change the first line of the stack trace.

```js
const err = new Error('The message');
console.log(err.message);
// Prints: The message
```

