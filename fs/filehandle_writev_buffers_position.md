<!-- YAML
added: v12.9.0
-->

* `buffers` {ArrayBufferView[]}
* `position` {integer}
* 返回: {Promise}

将 `ArrayBufferViews` 数组写入该文件。

`Promise` 会被解决并带上一个对象，对象包含一个 `bytesWritten` 属性（表明写入的字节数）和一个 `buffers` 属性（指向 `buffers` 输入）。

`position` 指定文件开头的偏移量（数据应该被写入的位置）。 
如果 `typeof position !== 'number'`，则数据会被写入当前的位置。 

在同一文件上多次调用 `writev()` 且不等待前面的操作完成，这是不安全的。

在 Linux 上，当以追加模式打开文件时，写入无法指定位置。 
内核会忽略位置参数，并始终将数据追加到文件的末尾。

