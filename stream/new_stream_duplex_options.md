<!-- YAML
changes:
  - version: v8.4.0
    pr-url: https://github.com/nodejs/node/pull/14636
    description: The `readableHighWaterMark` and `writableHighWaterMark` options
                 are supported now.
-->

* `options` {Object} 传给可读和可写流的构造函数，还有如下字段：
  * `allowHalfOpen` {boolean} 默认是`true`。如果设置为`false`, 那么当读端停止时，写端自动停止。
  * `readableObjectMode` {boolean} 默认是 `false`。会为流的读端设置`objectMode`。如果 `objectMode`是 `true`，那就没有任何用。
  * `writableObjectMode` {boolean} 默认是 `false`。会为流的写端设置`objectMode`。如果 `objectMode`是 `true`，那就没有任何用。
  * `readableHighWaterMark` {number} 设置 `highWaterMark` 可读流的缓冲区大小。 如果已经设置 `highWaterMark`则`readableHighWaterMark`不起作用。
  * `writableHighWaterMark` {number} 设置 `highWaterMark` 可写流缓冲区大小。如果设置了`highWaterMark` 则`writableHighWaterMark`不起作用。

例如:

```js
const { Duplex } = require('stream');

class MyDuplex extends Duplex {
  constructor(options) {
    super(options);
    // ...
  }
}
```

或者, 使用ES6之前的语法来创建构造函数:

```js
const { Duplex } = require('stream');
const util = require('util');

function MyDuplex(options) {
  if (!(this instanceof MyDuplex))
    return new MyDuplex(options);
  Duplex.call(this, options);
}
util.inherits(MyDuplex, Duplex);
```

又或者, 用简化的构造函数:

```js
const { Duplex } = require('stream');

const myDuplex = new Duplex({
  read(size) {
    // ...
  },
  write(chunk, encoding, callback) {
    // ...
  }
});
```

