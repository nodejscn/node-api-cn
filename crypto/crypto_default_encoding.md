<!-- YAML
added: v0.9.3
deprecated: v10.0.0
-->

> Stability: 0 - Deprecated

The default encoding to use for functions that can take either strings
or [buffers][`Buffer`]. The default value is `'buffer'`, which makes methods
default to [`Buffer`][] objects.

The `crypto.DEFAULT_ENCODING` mechanism is provided for backward compatibility
with legacy programs that expect `'latin1'` to be the default encoding.

New applications should expect the default to be `'buffer'`.

This property is deprecated.

