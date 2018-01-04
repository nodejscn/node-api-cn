* `options` {Object}
  * `highWaterMark` {number} 缓冲大小当开始调用[`stream.write()`][stream-write] 返回 `false`。默认`16384` (16kb), 对于 `objectMode` 流为默认为`16`。
  * `decodeStrings` {boolean} 是否解码字符串在调用 [`stream._write()`][stream-_write] 传递到缓冲区之前。默认为 `true`
  * `objectMode` {boolean} [`stream.write(anyObj)`][stream-write] 是否是一个有效的操作. 一旦设置,可以写字符串以外的值，例如`Buffer` 或者 `Uint8Array` 只要流支持。默认为`false`。
  * `write` {Function} 实现[`stream._write()`][stream-_write] 方法。
  * `writev` {Function} 实现[`stream._writev()`][stream-_writev] 方法。
  * `destroy` {Function} 实现[`stream._destroy()`][writable-_destroy] 方法。
  * `final` {Function} 实现[`stream._final()`][stream-_final] 方法。

例如：

```js
const { Writable } = require('stream');

class MyWritable extends Writable {
  constructor(options) {
    // Calls the stream.Writable() constructor
    super(options);
    // ...
  }
}
```

或者，使用ES6之前的语法来创建构造函数：

```js
const { Writable } = require('stream');
const util = require('util');

function MyWritable(options) {
  if (!(this instanceof MyWritable))
    return new MyWritable(options);
  Writable.call(this, options);
}
util.inherits(MyWritable, Writable);
```

或者，使用简化的构造函数方法:

```js
const { Writable } = require('stream');

const myWritable = new Writable({
  write(chunk, encoding, callback) {
    // ...
  },
  writev(chunks, callback) {
    // ...
  }
});
```
