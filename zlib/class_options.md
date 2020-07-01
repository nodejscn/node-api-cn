<!-- YAML
added: v0.11.1
changes:
  - version: v14.5.0
    pr-url: https://github.com/nodejs/node/pull/33516
    description: The `maxOutputLength` option is supported now.
  - version: v9.4.0
    pr-url: https://github.com/nodejs/node/pull/16042
    description: The `dictionary` option can be an `ArrayBuffer`.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12001
    description: The `dictionary` option can be an `Uint8Array` now.
  - version: v5.11.0
    pr-url: https://github.com/nodejs/node/pull/6069
    description: The `finishFlush` option is supported now.
-->

<!--type=misc-->

每一个类都有一个 `options` 对象。
所有的选项都不是必需的。

注意一些选项只与压缩相关，会被解压类忽视。

* `flush` {integer} **默认值:** `zlib.constants.Z_NO_FLUSH`。
* `finishFlush` {integer} **默认值:** `zlib.constants.Z_FINISH`。
* `chunkSize` {integer} **默认值:** `16 * 1024`。
* `windowBits` {integer}
* `level` {integer} (compression only)
* `memLevel` {integer} (compression only)
* `strategy` {integer} (compression only)
* `dictionary` {Buffer|TypedArray|DataView|ArrayBuffer} （只能是 deflate/inflate，默认是空目录）。
* `info` {boolean} （如果为 `true`，则返回一个包含 `buffer` 和 `engine` 的对象）。
* `maxOutputLength` {integer} Limits output size when using
  [convenience methods][]. **Default:** [`buffer.kMaxLength`][]

更多信息请查阅 [`deflateInit2` 和 `inflateInit2`][`deflateInit2` and `inflateInit2`] 文档。

