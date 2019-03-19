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

`offset` 决定 `buffer` 中要被写入的部位，`length` 是一个整数，指定要写入的字节数。

`position` 指定文件开头的偏移量（数据应该被写入的位置）。
如果 `typeof position !== 'number'`，则数据会被写入当前的位置。
参阅 pwrite(2)。

回调有三个参数 `(err, bytesWritten, buffer)`，其中 `bytesWritten` 指定 `buffer` 中被写入的字节数。

如果调用此方法的 [`util.promisify()`] 版本，则返回的 `Promise` 会返回具有 `bytesWritten` 和 `buffer` 属性的 `Object`。

在同一个文件上多次使用 `fs.write()` 且不等待回调是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。

在 Linux 上，当以追加模式打开文件时，写入无法指定位置。
内核会忽略位置参数，并始终将数据追加到文件的末尾。


