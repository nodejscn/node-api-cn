
Because of the internal mechanics of how the `process.nextTick()` queue and
the microtask queue that underlies Promises are implemented within V8 and
Node.js, it is possible for code running within a context to "escape" the
`timeout` set using `vm.runInContext()`, `vm.runInNewContext()`, and
`vm.runInThisContext()`.

For example, the following code executed by `vm.runInNewContext()` with a
timeout of 5 milliseconds schedules an infinite loop to run after a promise
resolves. The scheduled loop is never interrupted by the timeout:

```js
const vm = require('vm');

function loop() {
  while (1) console.log(Date.now());
}

vm.runInNewContext(
  'Promise.resolve().then(loop);',
  { loop, console },
  { timeout: 5 }
);
```

This issue also occurs when the `loop()` call is scheduled using
the `process.nextTick()` function.

This issue occurs because all contexts share the same microtask and nextTick
queues.























