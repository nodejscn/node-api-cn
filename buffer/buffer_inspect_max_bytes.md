<!-- YAML
added: v0.5.4
-->

* {Integer} **Default:** `50`

Returns the maximum number of bytes that will be returned when
`buf.inspect()` is called. This can be overridden by user modules. See
[`util.inspect()`] for more details on `buf.inspect()` behavior.

Note that this is a property on the `buffer` module as returned by
`require('buffer')`, not on the `Buffer` global or a `Buffer` instance.

