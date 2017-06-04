
As a best practice, warnings should be emitted only once per process. To do
so, it is recommended to place the `emitWarning()` behind a simple boolean
flag as illustrated in the example below:

```js
function emitMyWarning() {
  if (!emitMyWarning.warned) {
    emitMyWarning.warned = true;
    process.emitWarning('Only warn once!');
  }
}
emitMyWarning();
// Emits: (node: 56339) Warning: Only warn once!
emitMyWarning();
// Emits nothing
```

