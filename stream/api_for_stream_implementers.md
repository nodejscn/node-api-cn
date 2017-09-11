
<!--type=misc-->

`stream`模块API的设计是为了让JavaScript的原型继承模式可以简单的实现流。

首先，一个流开发者可能声明了一个JavaScript类并且继承四个基本流类中的一个（`stream.Weiteable`，`stream.Readable`，`stream.Duplex`，或者`stream.Transform`），确保他们调用合适的父类构造函数:

```js
const { Writable } = require('stream');

class MyWritable extends Writable {
  constructor(options) {
    super(options);
    // ...
  }
}
```

新的流类必须实现一个或多个特定的方法，根据所创建的流类型，如下图所示:

| 用例 | 类 | 实现的方法 |
| --- | --- | --- |
| 只读流 | [Readable](#stream_class_stream_readable) | [_read](#stream_readable_read_size_1) |
| 只写流 | [writable](#stream_class_stream_writable) | [_write](#stream_writable_write_chunk_encoding_callback_1) ，[_writev](#stream_writable_writev_chunks_callback)，[_final](#stream_writable_final_callback) |
| 可读可写流 | [Duplex](#stream_class_stream_duplex) | [_read](#stream_readable_read_size_1) ，[_write](#stream_writable_write_chunk_encoding_callback_1) ，[_writev](#stream_writable_writev_chunks_callback)，[_final](#stream_writable_final_callback) |
| 操作写数据，然后读结果 | [Transform](#stream_class_stream_transform) | [_transform](#stream_transform_transform_chunk_encoding_callback)，[_flush](#stream_transform_flush_callback)，[_final](#stream_writable_final_callback) |

注意：实现流的代码里面不应该出现调用“public”方法的地方因为这些方法是给使用者使用的（[流使用者](#stream_api_for_stream_consumers)部分的API所述）。这样做可能会导致使用流的应用程序代码产生不利的副作用。

