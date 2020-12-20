
`Promise`s and `async function`s can schedule tasks run by the JavaScript
engine asynchronously. By default, these tasks are run after all JavaScript
functions on the current stack are done executing.
This allows escaping the functionality of the `timeout` and
`breakOnSigint` options.

例如，`vm.runInNewContext()` 执行的以下代码（超时为 5 毫秒）会在 promise 解决后调度无限循环。 
调度的循环永远不会被超时中断：

```js
const vm = require('vm');

function loop() {
  console.log('entering loop');
  while (1) console.log(Date.now());
}

vm.runInNewContext(
  'Promise.resolve().then(() => loop());',
  { loop, console },
  { timeout: 5 }
);
// This is printed *before* 'entering loop' (!)
console.log('done executing');
```

This can be addressed by passing `microtaskMode: 'afterEvaluate'` to the code
that creates the `Context`:

```js
const vm = require('vm');

function loop() {
  while (1) console.log(Date.now());
}

vm.runInNewContext(
  'Promise.resolve().then(() => loop());',
  { loop, console },
  { timeout: 5, microtaskMode: 'afterEvaluate' }
);
```

In this case, the microtask scheduled through `promise.then()` will be run
before returning from `vm.runInNewContext()`, and will be interrupted
by the `timeout` functionality. This applies only to code running in a
`vm.Context`, so e.g. [`vm.runInThisContext()`][] does not take this option.

Promise callbacks are entered into the microtask queue of the context in which
they were created. For example, if `() => loop()` is replaced with just `loop`
in the above example, then `loop` will be pushed into the global microtask
queue, because it is a function from the outer (main) context, and thus will
also be able to escape the timeout.

If asynchronous scheduling functions such as `process.nextTick()`,
`queueMicrotask()`, `setTimeout()`, `setImmediate()`, etc. are made available
inside a `vm.Context`, functions passed to them will be added to global queues,
which are shared by all contexts. Therefore, callbacks passed to those functions
are not controllable through the timeout either.

