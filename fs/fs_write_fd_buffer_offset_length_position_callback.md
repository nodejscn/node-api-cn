<!-- YAML
added: v0.0.2
-->

* `fd` {Integer}
* `buffer` {String | Buffer}
* `offset` {Integer}
* `length` {Integer}
* `position` {Integer}
* `callback` {Function}

写入 `buffer` 到 `fd` 指定的文件。

`offset` 决定 buffer 中被写入的部分，`length` 是一个整数，指定要写入的字节数。

`position` 指向从文件开始写入数据的位置的偏移量。
如果 `typeof position !== 'number'`，则数据从当前位置写入。详见 pwrite(2)。

回调有三个参数 `(err, written, buffer)`，其中 `written` 指定从 `buffer` 写入了多少**字节**。

注意，多次对同一文件使用 `fs.write` 且不等待回调，是不安全的。
对于这种情况，强烈推荐使用 `fs.createWriteStream`。

在 Linux 上，当文件以追加模式打开时，指定位置的写入是不起作用的。
内核会忽略位置参数，并总是将数据追加到文件的末尾。

