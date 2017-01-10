
As a best practice, warnings should be emitted only once per process. To do
so, it is recommended to place the `emitWarning()` behind a simple boolean
flag as illustrated in the example below:

```js
var warned = false;
function emitMyWarning() {
  if (!warned) {
    process.emitWarning('Only warn once!');
    warned = true;
  }
}
emitMyWarning();
// Emits: (node: 56339) Warning: Only warn once!
emitMyWarning();
// Emits nothing
```

