
<!--type=misc-->

`stream` 模块 API 旨在为了更容易地使用 JavaScript 的原型继承模式来实现流。

首先，流的开发者声明一个新的 JavaScript 类，该类继承了四个基本流类之一（`stream.Writeable`、`stream.Readable`、`stream.Duplex` 或 `stream.Transform`），并确保调用了相应的父类构造函数:

<!-- eslint-disable no-useless-constructor -->
```js
const { Writable } = require('stream');

class MyWritable extends Writable {
  constructor({ highWaterMark, ...options }) {
    super({
      highWaterMark,
      autoDestroy: true,
      emitClose: true
    });
    // ...
  }
}
```

当继承流时，在传入基本构造函数之前，务必清楚使用者可以且应该提供哪些选项。 
例如，如果实现需要 `autoDestroy` 和 `emitClose` 选项，则不允许使用者覆盖这些选项。 
应明确要传入的选项，而不是隐式地传入所有选项。

新的流类必须实现一个或多个特定的方法，具体取决于要创建的流的类型，如下图所示:

| 用例 | 类 | 需要实现的方法 |
| -------- | ----- | ---------------------- |
| 只读 | [`Readable`] | [`_read()`][stream-_read] |
| 只写 | [`Writable`] | [`_write()`][stream-_write]、[`_writev()`][stream-_writev]、[`_final()`][stream-_final] |
| 可读可写 | [`Duplex`] | [`_read()`][stream-_read]、[`_write()`][stream-_write]、[`_writev()`][stream-_writev]、[`_final()`][stream-_final] |
| 对写入的数据进行操作，然后读取结果 | [`Transform`][] | [`_transform()`][stream-_transform]、[`_flush()`][stream-_flush]、[`_final()`][stream-_final] |

流的实现代码应永远不要调用旨在供消费者使用的公共方法（详见[用于消费流的API][API for Stream Consumers]）。
这样做可能会导致消费流的应用程序代码产生不利的副作用。

