
By default, promise executions are not assigned `asyncId`s due to the relatively
expensive nature of the [promise introspection API][PromiseHooks] provided by
V8. This means that programs using promises or `async`/`await` will not get
correct execution and trigger ids for promise callback contexts by default.

```js
const ah = require('async_hooks');
Promise.resolve(1729).then(() => {
  console.log(`eid ${ah.executionAsyncId()} tid ${ah.triggerAsyncId()}`);
});
// produces:
// eid 1 tid 0
```

Observe that the `then()` callback claims to have executed in the context of the
outer scope even though there was an asynchronous hop involved. Also note that
the `triggerAsyncId` value is `0`, which means that we are missing context about
the resource that caused (triggered) the `then()` callback to be executed.

Installing async hooks via `async_hooks.createHook` enables promise execution
tracking:

```js
const ah = require('async_hooks');
ah.createHook({ init() {} }).enable(); // forces PromiseHooks to be enabled.
Promise.resolve(1729).then(() => {
  console.log(`eid ${ah.executionAsyncId()} tid ${ah.triggerAsyncId()}`);
});
// produces:
// eid 7 tid 6
```

In this example, adding any actual hook function enabled the tracking of
promises. There are two promises in the example above; the promise created by
`Promise.resolve()` and the promise returned by the call to `then()`. In the
example above, the first promise got the `asyncId` `6` and the latter got
`asyncId` `7`. During the execution of the `then()` callback, we are executing
in the context of promise with `asyncId` `7`. This promise was triggered by
async resource `6`.

Another subtlety with promises is that `before` and `after` callbacks are run
only on chained promises. That means promises not created by `then()`/`catch()`
will not have the `before` and `after` callbacks fired on them. For more details
see the details of the V8 [PromiseHooks][] API.

