
<!--type=misc-->

`stream` 模块 API 的设计是为了更容易使用 JavaScript 的原型继承模式来实现流。

流的开发者可以声明一个新的 JavaScript 类并继承四个基本流类中之一（`stream.Writeable`、`stream.Readable`、`stream.Duplex` 或 `stream.Transform`），且确保调用了对应的父类构造器:

<!-- eslint-disable no-useless-constructor -->
```js
const { Writable } = require('stream');

class MyWritable extends Writable {
  constructor(options) {
    super(options);
    // ...
  }
}
```

根据所创建的流类型，新的流类必须实现一个或多个特定的方法，如下图所示:

| 用例 | 类 | 需实现的方法 |
| -------- | ----- | ---------------------- |
| 只读流 | [`Readable`] | <code>[_read][stream-_read]</code> |
| 只写流 | [`Writable`] | <code>[_write][stream-_write]</code>, <code>[_writev][stream-_writev]</code>, <code>[_final][stream-_final]</code> |
| 可读可写流 | [`Duplex`] | <code>[_read][stream-_read]</code>, <code>[_write][stream-_write]</code>, <code>[_writev][stream-_writev]</code>, <code>[_final][stream-_final]</code> |
| 对写入的数据进行操作，然后读取结果 | [`Transform`] | <code>[_transform][stream-_transform]</code>, <code>[_flush][stream-_flush]</code>, <code>[_final][stream-_final]</code> |

实现流的代码中不应该调用流的公共方法，因为这些方法是给消费者使用的（详见[用于消费流的API][API for Stream Consumers]）。
这样做可能会导致使用流的应用程序代码产生不利的副作用。

