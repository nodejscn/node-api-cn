<!-- YAML
added: v0.5.8
-->

<!--type=misc-->

All of the constants defined in `zlib.h` are also defined on `require('zlib')`.
In the normal course of operations, it will not be necessary to use these
constants. They are documented so that their presence is not surprising. This
section is taken almost directly from the [zlib documentation][].  See
<http://zlib.net/manual.html#Constants> for more details.

Allowed flush values.

* `zlib.Z_NO_FLUSH`
* `zlib.Z_PARTIAL_FLUSH`
* `zlib.Z_SYNC_FLUSH`
* `zlib.Z_FULL_FLUSH`
* `zlib.Z_FINISH`
* `zlib.Z_BLOCK`
* `zlib.Z_TREES`

Return codes for the compression/decompression functions. Negative
values are errors, positive values are used for special but normal
events.

* `zlib.Z_OK`
* `zlib.Z_STREAM_END`
* `zlib.Z_NEED_DICT`
* `zlib.Z_ERRNO`
* `zlib.Z_STREAM_ERROR`
* `zlib.Z_DATA_ERROR`
* `zlib.Z_MEM_ERROR`
* `zlib.Z_BUF_ERROR`
* `zlib.Z_VERSION_ERROR`

Compression levels.

* `zlib.Z_NO_COMPRESSION`
* `zlib.Z_BEST_SPEED`
* `zlib.Z_BEST_COMPRESSION`
* `zlib.Z_DEFAULT_COMPRESSION`

Compression strategy.

* `zlib.Z_FILTERED`
* `zlib.Z_HUFFMAN_ONLY`
* `zlib.Z_RLE`
* `zlib.Z_FIXED`
* `zlib.Z_DEFAULT_STRATEGY`

The deflate compression method (the only one supported in this version).

* `zlib.Z_DEFLATED`

For initializing zalloc, zfree, opaque.

* `zlib.Z_NULL`

