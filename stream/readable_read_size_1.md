<!-- YAML
added: v0.9.4
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17979
    description: call `_read()` only once per microtick
-->

* `size` {number} 要异步读取的字节数。

该函数不能被应用程序代码直接调用。
它应该由子类实现，且只能被内部的 `Readable` 类的方法调用。

所有可读流的实现必须提供 `readable._read()` 方法从底层资源获取数据。

当 `readable._read()` 被调用时，如果从资源读取到数据，则需要开始使用 [`this.push(dataChunk)`][stream-push] 推送数据到读取队列。
`_read()` 应该持续从资源读取数据并推送数据，直到 `readable.push()` 返回 `false`。
若想再次调用 `_read()` 方法，则需要恢复推送数据到队列。

一旦 `readable._read()` 被调用，它不会被再次调用，除非调用了 [`readable.push()`][stream-push]。
这是为了确保 `readable._read()` 在同步执行时只会被调用一次。

`size` 是可选的参数。
对于读取是一个单一操作的实现，可以使用 `size` 参数来决定要读取多少数据。
对于其他的实现，可以忽略这个参数，只要有数据就提供数据。
不需要等待指定 `size` 字节的数据在调用 [`stream.push(chunk)`][stream-push]。

`readable._read()` 方法有下划线前缀，因为它是在定义在类的内部，不应该被用户程序直接调用。
