<!-- YAML
added: v8.0.0
-->

Destroy the stream, and emit `'error'`. After this call, the
transform stream would release any internal resources.
implementors should not override this method, but instead implement
[`readable._destroy`][readable-_destroy].
The default implementation of `_destroy` for `Transform` also emit `'close'`.

