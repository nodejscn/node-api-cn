
A subclass of `Error` that indicates that a program is not valid JavaScript.
These errors may only be generated and propagated as a result of code
evaluation. Code evaluation may happen as a result of `eval`, `Function`,
`require`, or [vm][]. These errors are almost always indicative of a broken
program.

```js
try {
  require('vm').runInThisContext('binary ! isNotOk');
} catch(err) {
  // err will be a SyntaxError
}
```

`SyntaxError` instances are unrecoverable in the context that created them –
they may only be caught by other contexts.

