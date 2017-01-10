<!-- YAML
added: v0.9.3
-->

The default encoding to use for functions that can take either strings
or [buffers][`Buffer`]. The default value is `'buffer'`, which makes methods
default to [`Buffer`][] objects.

The `crypto.DEFAULT_ENCODING` mechanism is provided for backwards compatibility
with legacy programs that expect `'latin1'` to be the default encoding.

New applications should expect the default to be `'buffer'`. This property may
become deprecated in a future Node.js release.

