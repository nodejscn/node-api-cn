
<!-- type=misc -->

Any time an `Error` object is routed through a domain, a few extra fields
are added to it.

* `error.domain` The domain that first handled the error.
* `error.domainEmitter` The event emitter that emitted an `'error'` event
  with the error object.
* `error.domainBound` The callback function which was bound to the
  domain, and passed an error as its first argument.
* `error.domainThrown` A boolean indicating whether the error was
  thrown, emitted, or passed to a bound callback function.

