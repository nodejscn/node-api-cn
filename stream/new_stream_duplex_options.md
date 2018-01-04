<!-- YAML
changes:
  - version: v8.4.0
    pr-url: https://github.com/nodejs/node/pull/14636
    description: The `readableHighWaterMark` and `writableHighWaterMark` options
                 are supported now.
-->

* `options` {Object} Passed to both Writable and Readable
  constructors. Also has the following fields:
  传给可读和可写流的构造函数，还有如下字段：
  * `allowHalfOpen` {boolean} 默认是`true`.
    如果设置为`false`, 那么当读端停止时，写端自动停止。
  * `readableObjectMode` {boolean} 默认是 `false`。
    会为流的读端设置`objectMode`。
    如果 `objectMode`是 `true`，那就没有任何用。
  * `writableObjectMode` {boolean} 默认是 `false`。
    会为流的读端设置`objectMode`。
    如果 `objectMode`是 `true`，那就没有任何用。
  * `readableHighWaterMark` {number} Sets `highWaterMark` for the readable side
    of the stream. Has no effect if `highWaterMark` is provided.
  * `writableHighWaterMark` {number} Sets `highWaterMark` for the writable side
    of the stream. Has no effect if `highWaterMark` is provided.

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

