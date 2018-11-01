
<!--type=misc-->

`stream` 模块 API 的设计是为了更容易使用 JavaScript 的原型继承模式来实现流。

流的开发者可以声明一个新的 JavaScript 类并继承四个基本流类中之一（`stream.Writeable`、`stream.Readable`、`stream.Duplex` 或 `stream.Transform`），且确保调用了对应的父类构造器:

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

| 用例 | 类 | 需实现的方法 |
| -------- | ----- | ---------------------- |
| 只读的流 | [`Readable`] | <code>[_read][stream-_read]</code> |
| 只写的流 | [`Writable`] | <code>[_write][stream-_write]</code>, <code>[_writev][stream-_writev]</code>, <code>[_final][stream-_final]</code> |
| 可读可写的流 | [`Duplex`] | <code>[_read][stream-_read]</code>, <code>[_write][stream-_write]</code>, <code>[_writev][stream-_writev]</code>, <code>[_final][stream-_final]</code> |
| 可操作写入得数据并读取结果的流 | [`Transform`] | <code>[_transform][stream-_transform]</code>, <code>[_flush][stream-_flush]</code>, <code>[_final][stream-_final]</code> |

注意：实现流的代码里面不应该出现调用“public”方法的地方因为这些方法是给使用者使用的（[流使用者](#stream_api_for_stream_consumers)部分的API所述）。这样做可能会导致使用流的应用程序代码产生不利的副作用。

