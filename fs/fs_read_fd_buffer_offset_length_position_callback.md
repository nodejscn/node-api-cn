<!-- YAML
added: v0.0.2
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22150
    description: The `buffer` parameter can now be any `TypedArray`, or a
                 `DataView`.
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: The `buffer` parameter can now be a `Uint8Array`.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/4518
    description: The `length` parameter can now be `0`.
-->

* `fd` {integer}
* `buffer` {Buffer|TypedArray|DataView}
* `offset` {integer}
* `length` {integer}
* `position` {integer}
* `callback` {Function}
  * `err` {Error}
  * `bytesRead` {integer}
  * `buffer` {Buffer}

从 `fd` 指定的文件中读取数据。

`buffer` 是数据将被写入到的 buffer。

`offset` 是 buffer 中开始写入的偏移量。

`length` 是一个整数，指定要读取的字节数。

`position` 指定从文件中开始读取的位置。
如果 `position` 为 `null`，则数据从当前文件读取位置开始读取，且文件读取位置会被更新。
如果 `position` 为一个整数，则文件读取位置保持不变。

回调有三个参数 `(err, bytesRead, buffer)`。

