<!-- YAML
added: v0.11.1
-->

<!--type=misc-->

Each class takes an `options` object.  All options are optional.

Note that some options are only relevant when compressing, and are
ignored by the decompression classes.

* `flush` (default: `zlib.Z_NO_FLUSH`)
* `finishFlush` (default: `zlib.Z_FINISH`)
* `chunkSize` (default: 16*1024)
* `windowBits`
* `level` (compression only)
* `memLevel` (compression only)
* `strategy` (compression only)
* `dictionary` (deflate/inflate only, empty dictionary by default)

See the description of `deflateInit2` and `inflateInit2` at
<http://zlib.net/manual.html#Advanced> for more information on these.

