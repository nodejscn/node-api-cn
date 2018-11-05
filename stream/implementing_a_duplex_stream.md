
[双工流]同时实现了[可读流]和[可写流]，例如 TCP socket 连接。
因为 JavaScript 不支持多重继承，所以使用 `stream.Duplex` 类实现[双工流]（而不是使用 `stream.Readable` 类和 `stream.Writable` 类）。

`stream.Duplex` 类的原型继承自 `stream.Readable` 和寄生自 `stream.Writable`，但是 `instanceof` 对这两个基础类都可用，因为重写了 `stream.Writable` 的 [`Symbol.hasInstance`]。

自定义的双工流必须调用 `new stream.Duplex([options])` 构造函数并实现 `readable._read()` 和 `writable._write()` 方法。
