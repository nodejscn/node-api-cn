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

每一个类都有一个 `options` 对象. 所有的选项都是可选的.

注意一些选项只与压缩相关, 会被解压类忽视.

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

更多信息查阅在 <http://zlib.net/manual.html#Advanced> 关于 `deflateInit2` 以及 `inflateInit2` 的描述， 
