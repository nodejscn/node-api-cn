
* `options` {Object}
  * `highWaterMark` {number} 从底层资源读取数据并存储在内部缓冲区中的最大[字节数][hwm-gotcha]。
    默认为 `16384` (16kb), 对象模式的流默认为 `16`。
  * `encoding` {string} 如果指定了，则使用指定的字符编码将 buffer 解码成字符串。
    默认为 `null`。
  * `objectMode` {boolean} 流是否可以是一个对象流。
    也就是说 [`stream.read(n)`][stream-read] 会返回对象而不是 `Buffer`。
    默认为 `false`。
  * `read` {Function} 对 [`stream._read()`][stream-_read] 方法的实现。
  * `destroy` {Function} 对 [`stream._destroy()`][readable-_destroy] 方法的实现。

<!-- eslint-disable no-useless-constructor -->
```js
const { Readable } = require('stream');

class MyReadable extends Readable {
  constructor(options) {
    // 调用 stream.Readable(options) 构造函数。
    super(options);
    // ...
  }
}
```

使用 ES6 之前的语法：

```js
const { Readable } = require('stream');
const util = require('util');

function MyReadable(options) {
  if (!(this instanceof MyReadable))
    return new MyReadable(options);
  Readable.call(this, options);
}
util.inherits(MyReadable, Readable);
```

使用简化的构造函数：

```js
const { Readable } = require('stream');

const myReadable = new Readable({
  read(size) {
    // ...
  }
});
```
