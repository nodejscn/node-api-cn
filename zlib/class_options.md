<!-- YAML
added: v0.11.1
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12001
    description: The `dictionary` option can be an Uint8Array now.
  - version: v5.11.0
    pr-url: https://github.com/nodejs/node/pull/6069
    description: The `finishFlush` option is supported now.
-->

<!--type=misc-->

Each class takes an `options` object.  All options are optional.

Note that some options are only relevant when compressing, and are
ignored by the decompression classes.

* `flush` {integer} (default: `zlib.constants.Z_NO_FLUSH`)
* `finishFlush` {integer} (default: `zlib.constants.Z_FINISH`)
* `chunkSize` {integer} (default: 16\*1024)
* `windowBits` {integer}
* `level` {integer} (compression only)
* `memLevel` {integer} (compression only)
* `strategy` {integer} (compression only)
* `dictionary` {Buffer|TypedArray|DataView} (deflate/inflate only, empty dictionary by
  default)
* `info` {boolean} (If `true`, returns an object with `buffer` and `engine`)

See the description of `deflateInit2` and `inflateInit2` at
<http://zlib.net/manual.html#Advanced> for more information on these.

