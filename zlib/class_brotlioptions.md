<!-- YAML
added: v11.7.0
changes:
  - version:
    - v14.5.0
    - v12.19.0
    pr-url: https://github.com/nodejs/node/pull/33516
    description: The `maxOutputLength` option is supported now.
-->

<!--type=misc-->

Each Brotli-based class takes an `options` object. All options are optional.

* `flush` {integer} **Default:** `zlib.constants.BROTLI_OPERATION_PROCESS`
* `finishFlush` {integer} **Default:** `zlib.constants.BROTLI_OPERATION_FINISH`
* `chunkSize` {integer} **Default:** `16 * 1024`
* `params` {Object} Key-value object containing indexed [Brotli parameters][].
* `maxOutputLength` {integer} Limits output size when using
  [convenience methods][]. **Default:** [`buffer.kMaxLength`][]

For example:

```js
const stream = zlib.createBrotliCompress({
  chunkSize: 32 * 1024,
  params: {
    [zlib.constants.BROTLI_PARAM_MODE]: zlib.constants.BROTLI_MODE_TEXT,
    [zlib.constants.BROTLI_PARAM_QUALITY]: 4,
    [zlib.constants.BROTLI_PARAM_SIZE_HINT]: fs.statSync(inputFile).size
  }
});
```

