<!-- YAML
added: v12.9.0
-->

* `fd` {integer}
* `buffers` {ArrayBufferView[]}
* `position` {integer}
* `callback` {Function}
  * `err` {Error}
  * `bytesWritten` {integer}
  * `buffers` {ArrayBufferView[]}

使用 `writev()` 将一个 `ArrayBufferView` 数组写入 `fd` 指定的文件。

`position` 指定文件开头的偏移量（数据要被写入的位置）。 
如果 `typeof position !== 'number'`，则数据会被写入当前的位置。 

回调有三个参数：`err`、`bytesWritten` 和 `buffers`。 
`bytesWritten` 是从 `buffers` 写入的字节数。

如果此方法是 [`util.promisify()`] 化的版本，则它返回的 `Promise` 会返回具有 `bytesWritten` 和 `buffers` 属性的 `Object`。

不等待回调就对同一个文件多次使用 `fs.writev()` 是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。


在 Linux 上，当以追加模式打开文件时，则写入时无法指定位置。 
内核会忽略位置参数，并始终追加数据到文件的末尾。

