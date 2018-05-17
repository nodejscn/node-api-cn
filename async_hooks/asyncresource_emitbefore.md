<!-- YAML
deprecated: v9.6.0
-->
> Stability: 0 - Deprecated: Use [`asyncResource.runInAsyncScope()`][] instead.

Call all `before` callbacks to notify that a new asynchronous execution context
is being entered. If nested calls to `emitBefore()` are made, the stack of
`asyncId`s will be tracked and properly unwound.

`before` and `after` calls must be unwound in the same order that they
are called. Otherwise, an unrecoverable exception will occur and the process
will abort. For this reason, the `emitBefore` and `emitAfter` APIs are
considered deprecated. Please use `runInAsyncScope`, as it provides a much safer
alternative.

