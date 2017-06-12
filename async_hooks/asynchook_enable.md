
* Returns {AsyncHook} A reference to `asyncHook`.

Enable the callbacks for a given `AsyncHook` instance. If no callbacks are
provided enabling is a noop.

The `AsyncHook` instance is by default disabled. If the `AsyncHook` instance
should be enabled immediately after creation, the following pattern can be used.

```js
const async_hooks = require('async_hooks');

const hook = async_hooks.createHook(callbacks).enable();
```

