<!-- YAML
added: v10.0.0
-->
* `buffer` {Buffer|Uint8Array}
* `offset` {integer}
* `length` {integer}
* `position` {integer}
* 返回: {Promise}

从文件中读取数据。

`buffer` 是数据将写入的缓冲区。

`offset` 是 buffer 中开始写入的偏移量。

`length` 是整数，指定要读取的字节数。

`position` 参数指定从文件中开始读取的位置。
如果 `position` 为 `null`，则从当前文件位置读取数据，并更新文件位置。
如果 `position` 是整数，则文件位置会保持不变。

成功读取之后，`Promise` 会被解决并带上一个对象，对象上有一个 `bytesRead` 属性（指定读取的字节数）和一个 `buffer` 属性（指向传入的 `buffer` 参数）。

如果文件没有被同时地修改，则当读取的字节数为零时，即到达文件的末尾。
