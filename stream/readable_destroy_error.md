<!-- YAML
added: v8.0.0
-->

Destroy the stream, and emit `'error'`. After this call, the
readable stream will release any internal resources.
Implementors should not override this method, but instead implement
[`readable._destroy`][readable-_destroy].

