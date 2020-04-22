<!-- YAML
added: v10.0.0
changes:
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/31030
    description: The `buffer` parameter won't coerce unsupported input to
                 buffers anymore.
-->
* `buffer` {Buffer|Uint8Array}
* `offset` {integer}
* `length` {integer}
* `position` {integer}
* 返回: {Promise}

将 `buffer` 写入到文件。

`Promise` 会被解决并带上一个对象，对象包含一个 `bytesWritten` 属性（指定写入的字节数）和一个 `buffer` 属性（指向写入的 `buffer`）。

`offset` 决定 buffer 中要被写入的部位，`length` 是一个整数，指定要写入的字节数。

`position` 指定文件开头的偏移量（数据应该被写入的位置）。
如果 `typeof position !== 'number'`，则数据会被写入当前的位置。
参阅 pwrite(2)。

在同一个文件上多次使用 `filehandle.write()` 且不等待 `Promise` 被解决（或被拒绝）是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。

在 Linux 上，当以追加模式打开文件时，写入无法指定位置。
内核会忽略位置参数，并始终将数据追加到文件的末尾。

