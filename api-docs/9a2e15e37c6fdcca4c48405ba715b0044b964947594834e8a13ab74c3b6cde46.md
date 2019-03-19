<!-- YAML
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18438
    description: >
      Add `emitClose` option to specify if `'close'` is emitted on destroy
-->

* `options` {Object}
  * `highWaterMark` {number} 当调用 [`stream.write()`][stream-write] 开始返回 `false` 时的缓冲大小。
    默认为 `16384` (16kb), 对象模式的流默认为 `16`。
  * `decodeStrings` {boolean} 是否把传入 [`stream._write()`][stream-_write] 的字符串编码为 `Buffer`，使用的字符编码为调用 [`stream.write()`][stream-write] 时指定的。
    默认为 `true`。
  * `defaultEncoding` {string} 当 [`stream.write()`][stream-write] 的参数没有指定字符编码时默认的字符编码。
    默认为 `'utf8'`。
  * `objectMode` {boolean} 是否可以调用 [`stream.write(anyObj)`][stream-write]。
    一旦设为 `true`，则除了字符串、`Buffer` 或 `Uint8Array`，还可以写入流实现支持的其他 JavaScript 值。
    默认为 `false`。
  * `emitClose` {boolean} 流被销毁后是否触发 `'close'` 事件。
    默认为 `true`。
  * `write` {Function} 对 [`stream._write()`][stream-_write] 方法的实现。
  * `writev` {Function} 对 [`stream._writev()`][stream-_writev] 方法的实现。
  * `destroy` {Function} 对 [`stream._destroy()`][writable-_destroy] 方法的实现。
  * `final` {Function} 对 [`stream._final()`][stream-_final] 方法的实现。

例子：

<!-- eslint-disable no-useless-constructor -->
```js
const { Writable } = require('stream');

class MyWritable extends Writable {
  constructor(options) {
    // 调用 stream.Writable() 构造函数。
    super(options);
    // ...
  }
}
```

使用 ES6 之前的语法：

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

使用简化的构造函数：

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

