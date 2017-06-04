
所有使用 Node.js API 创建的流对象都只能操作 strings 和 `Buffer`（或 `Uint8Array`）
对象。但是，通过一些第三方流的实现，你依然能够处理其它类型的 JavaScript 值 (除了 `null`，它在流处理中有特殊意义)。 这些流被认为是工作在 “对象模式”（object mode）。

在创建流的实例时，可以通过 `objectMode` 选项使流的实例切换到对象模式。试图将已经存在的流切换到对象模式是不安全的。

