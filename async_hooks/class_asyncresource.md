
The class `AsyncResource` was designed to be extended by the embedder's async
resources. Using this users can easily trigger the lifetime events of their
own resources.

The `init` hook will trigger when an `AsyncResource` is instantiated.

It is important that `before`/`after` calls are unwound
in the same order they are called. Otherwise an unrecoverable exception
will occur and node will abort.

The following is an overview of the `AsyncResource` API.

```js
const { AsyncResource } = require('async_hooks');

// AsyncResource() is meant to be extended. Instantiating a
// new AsyncResource() also triggers init. If triggerAsyncId is omitted then
// async_hook.executionAsyncId() is used.
const asyncResource = new AsyncResource(type, triggerAsyncId);

// Call AsyncHooks before callbacks.
asyncResource.emitBefore();

// Call AsyncHooks after callbacks.
asyncResource.emitAfter();

// Call AsyncHooks destroy callbacks.
asyncResource.emitDestroy();

// Return the unique ID assigned to the AsyncResource instance.
asyncResource.asyncId();

// Return the trigger ID for the AsyncResource instance.
asyncResource.triggerAsyncId();
```

