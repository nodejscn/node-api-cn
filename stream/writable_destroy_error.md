<!-- YAML
added: v8.0.0
-->

Destroy the stream, and emit the passed error. After this call, the
writible stream has ended. Implementors should not override this method,
but instead implement [`writable._destroy`][writable-_destroy].

