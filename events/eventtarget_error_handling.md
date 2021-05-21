
When a registered event listener throws (or returns a Promise that rejects),
by default the error is treated as an uncaught exception on
`process.nextTick()`. This means uncaught exceptions in `EventTarget`s will
terminate the Node.js process by default.

Throwing within an event listener will *not* stop the other registered handlers
from being invoked.

The `EventTarget` does not implement any special default handling for `'error'`
type events like `EventEmitter`.

Currently errors are first forwarded to the `process.on('error')` event
before reaching `process.on('uncaughtException')`. This behavior is
deprecated and will change in a future release to align `EventTarget` with
other Node.js APIs. Any code relying on the `process.on('error')` event should
be aligned with the new behavior.

