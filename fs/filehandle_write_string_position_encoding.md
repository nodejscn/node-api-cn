<!-- YAML
added: v10.0.0
-->

* `string` {string}
* `position` {integer}
* `encoding` {string} **默认值:** `'utf8'`。
* 返回: {Promise}

将 `string` 写入到文件。
如果 `string` 不是一个字符串，则该值会被强制转换为字符串。


`Promise` 会被解决并带上一个对象，对象包含一个 `bytesWritten` 属性（指定写入的字节数）和一个 `buffer` 属性（指向写入的 `string`）。

`position` 指定文件开头的偏移量（数据应该被写入的位置）。
如果 `position` 的类型不是一个 `number`，则数据会被写入当前的位置。
参阅 pwrite(2)。

`encoding` 是期望的字符串编码。

在同一个文件上多次使用 `filehandle.write()` 且不等待 `Promise` 被解决（或被拒绝）是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。

在 Linux 上，当以追加模式打开文件时，写入无法指定位置。
内核会忽略位置参数，并始终将数据追加到文件的末尾。

