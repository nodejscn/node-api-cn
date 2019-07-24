<!-- YAML
deprecated: v9.6.0
-->
> Stability: 0 - Deprecated: Use [`asyncResource.runInAsyncScope()`][] instead.

Call all `after` callbacks. If nested calls to `emitBefore()` were made, then
make sure the stack is unwound properly. Otherwise an error will be thrown.

If the user's callback throws an exception, `emitAfter()` will automatically be
called for all `asyncId`s on the stack if the error is handled by a domain or
`'uncaughtException'` handler.

`before` and `after` calls must be unwound in the same order that they
are called. Otherwise, an unrecoverable exception will occur and the process
will abort. For this reason, the `emitBefore` and `emitAfter` APIs are
considered deprecated. Please use `runInAsyncScope`, as it provides a much safer
alternative.

