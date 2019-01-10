
* `id` {integer} 一个32位的无符号整型。
* `arrayBuffer` {ArrayBuffer} 一个`ArrayBuffer`实例。

标记一个`ArrayBuffer`, 表明它的内容正在被带外传输中。同时将`ArrayBuffer`包裹于一个反序列化的上下文内，之后将结果传入[`deserializer.transferArrayBuffer()`][]中。

