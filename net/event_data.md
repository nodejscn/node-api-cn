<!-- YAML
added: v0.1.90
-->

* {Buffer}

当接收到数据时被触发。 参数 `data` 是 `Buffer` 或者 `String` 类型。
数据的编码由`socket.setEncoding()`设定。（查看 [Readable Stream][]一节获取更多信息）

注意：如果当`Socket`触发`'data'`事件时，没有监听器在监听，这导致 **数据可能会丢失**。

