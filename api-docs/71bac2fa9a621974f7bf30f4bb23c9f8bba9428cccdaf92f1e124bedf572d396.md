
* `id` {integer} 一个 32 位无符号整型
* `arrayBuffer` {ArrayBuffer|SharedArrayBuffer} `ArrayBuffer`实例

标记一个`ArrayBuffer`, 表明它的内容正在被带外传输中。同时将`ArrayBuffer`包裹于一个序列化的上下文内，之后将结果传入[`serializer.transferArrayBuffer()`][]中（当`arrayBuffer`是`ShareArrayBuffer`实例时，返回[`serializer._getSharedArrayBufferId()`][]产生的`id`）
