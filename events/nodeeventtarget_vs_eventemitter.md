
The `NodeEventTarget` object implements a modified subset of the
`EventEmitter` API that allows it to closely *emulate* an `EventEmitter` in
certain situations. A `NodeEventTarget` is *not* an instance of `EventEmitter`
and cannot be used in place of an `EventEmitter` in most cases.

1. Unlike `EventEmitter`, any given `listener` can be registered at most once
   per event `type`. Attempts to register a `listener` multiple times are
   ignored.
2. The `NodeEventTarget` does not emulate the full `EventEmitter` API.
   Specifically the `prependListener()`, `prependOnceListener()`,
   `rawListeners()`, `setMaxListeners()`, `getMaxListeners()`, and
   `errorMonitor` APIs are not emulated. The `'newListener'` and
   `'removeListener'` events will also not be emitted.
3. The `NodeEventTarget` does not implement any special default behavior
   for events with type `'error'`.
3. The `NodeEventTarget` supports `EventListener` objects as well as
   functions as handlers for all event types.

