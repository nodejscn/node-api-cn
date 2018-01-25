
* `chunk` {Buffer|string|any} 被转换的数据块。它总是一个buffer除非在option中配置`decodeString`为`false`或者当前流处在`object mode`下。
* `encoding` {string} 如果 chunk 是字符串，那么encoding就是该字符串的字符编码。如果块是Buffer，它是一个特殊的值'buffer',这种情况encoding可以被忽略。
* `callback` {Function} 当块被处理完成时调用此函数（包含error和data参数）。

*注意*：此函数不得直接由应用程序代码调用。它应该由子类实现，并由内部的Readable类方法调用。

所有的变换流的执行必须提供一个`_transform()`方法接收输入并提供输出。`transform._transform()`的实现会处理写入的字节，做某种计算并输出，然后使用`readable.push()`方法把这个输出传递到可读流。

从一个单个输入数据块可能会调用零次或多次`transform.push()`方法，调用次数取决于每次把多少数据做为一个输出结果。

有可能从任意给定输入的数据块中没有产生任何输出。

`callback` 会在当前数据被完全消费之后调用。在处理过程输入的过程中如果出错了,第一个参数是一个错误对象，没有出错Error参数则为null。如果传递第二个参数，它会被转发到`readable.push()`中。就像下面的例子：

```js
transform.prototype._transform = function(data, encoding, callback) {
  this.push(data);
  callback();
};

transform.prototype._transform = function(data, encoding, callback) {
  callback(null, data);
};
```

`transform._transform()` 方法前缀为下划线，因为它是定义在它的类的内部，不应该直接被用户程序调用。

`transform._transform()` 方法永远不能并行调用；流使用了队列机制，不论同步或者异步情况下，都必须先调用callback之后才能接收下一个数据。
