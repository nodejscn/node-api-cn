<!-- YAML
added: v0.0.2
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22150
    description: The `buffer` parameter can now be any `TypedArray` or a
                 `DataView`
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: The `buffer` parameter can now be a `Uint8Array`.
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/7856
    description: The `offset` and `length` parameters are optional now.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
-->

* `fd` {integer}
* `buffer` {Buffer|TypedArray|DataView}
* `offset` {integer}
* `length` {integer}
* `position` {integer}
* `callback` {Function}
  * `err` {Error}
  * `bytesWritten` {integer}
  * `buffer` {Buffer|TypedArray|DataView}

将 `buffer` 写入到 `fd` 指定的文件。

`offset` 指定 `buffer` 中要开始被写入的偏移量，`length` 指定要写入的字节数。

`position` 指定文件中要开始写入的偏移量。
如果 `typeof position !== 'number'`，则从当前位置开始写入。参见 pwrite(2)。

`callback` 有三个参数 `(err, bytesWritten, buffer)`，其中 `bytesWritten` 指定 `buffer` 中已写入文件的字节数。

对同一文件多次使用 `fs.write()` 且不等待回调，是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。

在 Linux 上，当以追加模式打开文件时，不能指定写入的位置。
内核会忽略位置参数，总是将数据追加到文件的尾部。


