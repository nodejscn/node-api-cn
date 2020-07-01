
Event listeners triggered by an [`EventEmitter`][] may be run in a different
execution context than the one that was active when `eventEmitter.on()` was
called.

The following example shows how to use the `AsyncResource` class to properly
associate an event listener with the correct execution context. The same
approach can be applied to a [`Stream`][] or a similar event-driven class.

```js
const { createServer } = require('http');
const { AsyncResource, executionAsyncId } = require('async_hooks');

const server = createServer((req, res) => {
  const asyncResource = new AsyncResource('request');
  // The listener will always run in the execution context of `asyncResource`.
  req.on('close', asyncResource.runInAsyncScope.bind(asyncResource, () => {
    // Prints: true
    console.log(asyncResource.asyncId() === executionAsyncId());
  }));
  res.end();
}).listen(3000);
```

