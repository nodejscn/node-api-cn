<!-- YAML
added: v0.1.21
changes:
  - version: v14.12.0
    pr-url: https://github.com/nodejs/node/pull/34993
    description: The `buffer` parameter will stringify an object with an
                 explicit `toString` function.
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/31030
    description: 参数 `buffer` 不再强制把不支持的输入转换为字符串。
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22150
    description: 参数 `buffer` 可以是任何 `TypedArray` 或 `DataView`。
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: 参数 `buffer` 可以是 `Uint8Array`。
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/7856
    description: 参数 `offset` 和 `length` 是可选的。
-->

* `fd` {integer}
* `buffer` {Buffer|TypedArray|DataView|string|Object}
* `offset` {integer}
* `length` {integer}
* `position` {integer}
* 返回: {number} 写入的字节数。

详见此 API 的异步版本的文档：[`fs.write(fd, buffer...)`]。

