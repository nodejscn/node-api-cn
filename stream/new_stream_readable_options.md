
* `options` {Object}
  * `highWaterMark` {number} 从底层资源读取数据并存储在内部缓冲区中的最大字节数。默认`16384` (16kb), 或者 `16`对应`objectMode`流模式。
  * `encoding` {string} 指定解析的字符编码格式. 默认 为`null`
  * `objectMode` {boolean} 一个对象的流。 这意味着 [`stream.read(n)`][stream-read] 返回的是一个单一的对象而不是n个字节的缓冲区。默认 `false`
  * `read` {Function} 对 [`stream._read()`][stream-_read]方法的实现。
  * `destroy` {Function} 对 [`stream._destroy()`][readable-_destroy] 方法的实现。

例如：

```js
const { Readable } = require('stream');

class MyReadable extends Readable {
  constructor(options) {
    // Calls the stream.Readable(options) constructor
    super(options);
    // ...
  }
}
```

或者使用ES6语法:

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

或者使用简化的构造方法：

```js
const { Readable } = require('stream');

const myReadable = new Readable({
  read(size) {
    // ...
  }
});
```
