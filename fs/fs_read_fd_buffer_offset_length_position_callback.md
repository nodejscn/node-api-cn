<!-- YAML
added: v0.0.2
changes:
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: The `buffer` parameter can now be a `Uint8Array`.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/4518
    description: The `length` parameter can now be `0`.
-->

* `fd` {integer}
* `buffer` {Buffer|Uint8Array}
* `offset` {integer}
* `length` {integer}
* `position` {integer}
* `callback` {Function}

从 `fd` 指定的文件中读取数据。

`buffer` 是数据将被写入到的 buffer。

`offset` 是 buffer 中开始写入的偏移量。

`length` 是一个整数，指定要读取的字节数。

`position` 是一个整数，指定从文件中开始读取的位置。
如果 `position` 为 `null`，则数据从当前文件位置开始读取。

回调有三个参数 `(err, bytesRead, buffer)`。

If this method is invoked as its [`util.promisify()`][]ed version, it returns
a Promise for an object with `bytesRead` and `buffer` properties.

