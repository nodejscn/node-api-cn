<!-- YAML
added: v0.1.21
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22150
    description: 参数 `buffer` 可以是任何 `TypedArray` 或 `DataView`。
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/4518
    description: 参数 `length` 可以为 `0`。
-->

* `fd` {integer}
* `buffer` {Buffer|TypedArray|DataView}
* `offset` {integer}
* `length` {integer}
* `position` {integer}
* 返回: {number}

返回 `bytesRead` 的数量。

有关详细信息，请参见此 API 异步版本的文档：[`fs.read()`]。

