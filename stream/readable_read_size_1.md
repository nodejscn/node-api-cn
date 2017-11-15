
* `size` {number} 异步读取的字节数。

*注意*: 这个函数不能直接被应用程序代码调用。 它应由子类实现，并仅能由Readable对象内部方法调用。

所有实现可读流的实例必须实现`readable._read()` 方法去获得底层的数据资源。

当 `readable._read()` 被调用，如果读取的数据是可用的，应该在最开始的实现的时候使用[`this.push(dataChunk)`][stream-push]方法将该数据推入读取队列。`_read()` 应该一直读取资源直到推送数据方法`readable.push()`返回`false`的时候停止。想再次调用`_read()`方法，需要再次往可读流里面push数据。

*注意*：一旦`readable._read()`方法被调用，只有在 [`readable.push()`][stream-push]方法被调用之后，才能再次被调用。

`size` 可选参数。`_read()`方法是一个实现读取数据的单操作，设置`size`参数来确定要读取数据的大小。 其他的实现可能会忽略这个参数，只要数据可用就提供数据。 不需要等到[`stream.push(chunk)`][stream-push]方法推入一定`size`的数据后才能调用。

`readable._read()`方法的前缀是一个下划线，因为它是在定义它的类的内部，不应该被直接调用用户程序。
