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

`buffer` 指定要写入数据的 buffer。

`offset` 指定 buffer 中开始写入的偏移量。

`length` 指定要读取的字节数。

`position` 指定文件中开始读取的偏移量。
如果 `position` 为 `null`，则从文件的当前位置开始读取。

`callback` 有三个参数 `(err, bytesRead, buffer)`。

如果使用 [`util.promisify()`] 版本，则 `Promise` 返回一个包含 `bytesRead` 和 `buffer` 的对象。

