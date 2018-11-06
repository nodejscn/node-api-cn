
* `chunk` {Buffer|string|any} 要转换的数据块。
   `chunk` 总会是一个 buffer，除非 `decodeStrings` 选项设为 `false` 或者流处在对象模式。
* `encoding` {string} 如果 `chunk` 是字符串，则 `encoding` 是字符串的字符编码。
   如果 `chunk` 是 buffer，则 `encoding` 的值为 'buffer'。
* `callback` {Function} 当 `chunk` 处理完成时的回调函数。

该函数不能被应用程序代码直接调用。
它应该由子类实现，且只能被内部的 `Readable` 类的方法调用。



所有转换流的实现都必须提供 `_transform()` 方法来接收输入并生产输出。
`transform._transform()` 的实现会处理写入的字节，进行一些计算操作，然后使用 `readable.push()` 输出到可读流。

`transform.push()` 可能会被调用零次或多次用来从每次输入的数据块产生输出，调用的次数取决需要多少数据来产生输出的结果。

输入的数据块有可能不会产生任何输出。

当前数据被完全消费之后，必须调用 `callback` 函数。
当处理输入的过程中发生出错时，`callback` 的第一个参数传入 `Error` 对象，否则传入 `null`。
如果 `callback` 传入了第二个参数，则它会被转发到 `readable.push()`。
就像下面的例子：

```js
transform.prototype._transform = function(data, encoding, callback) {
  this.push(data);
  callback();
};

transform.prototype._transform = function(data, encoding, callback) {
  callback(null, data);
};
```

`transform._transform()` 方法有下划线前缀，因为它是在定义在类的内部，不应该被用户程序直接调用。

`transform._transform()` 不能并行调用。
流使用了队列机制，无论同步或异步的情况下，都必须先调用 `callback` 之后才能接收下一个数据块。
