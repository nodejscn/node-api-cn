<!-- YAML
added: v8.0.0
-->

* Returns: `this`

Destroy the stream, and emit the passed error. After this call, the
writable stream has ended. Implementors should not override this method,
but instead implement [`writable._destroy`][writable-_destroy].

