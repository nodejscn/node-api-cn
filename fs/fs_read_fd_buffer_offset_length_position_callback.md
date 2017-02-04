<!-- YAML
added: v0.0.2
-->

* `fd` {Integer}
* `buffer` {String | Buffer}
* `offset` {Integer}
* `length` {Integer}
* `position` {Integer}
* `callback` {Function}

从 `fd` 指定的文件中读取数据。

`buffer` 是数据将被写入到的 buffer。

`offset` 是 buffer 中开始写入的偏移量。

`length` 是一个整数，指定要读取的字节数。

`position` 是一个整数，指定从文件中开始读取的位置。
如果 `position` 为 `null`，则数据从当前文件位置开始读取。

回调有三个参数 `(err, bytesRead, buffer)`。

