<!-- YAML
changes:
  - version: v8.4.0
    pr-url: https://github.com/nodejs/node/pull/14636
    description: The `readableHighWaterMark` and `writableHighWaterMark` options
                 are supported now.
-->

* `options` {Object} 同时传给 `Writable` 和 `Readable` 的构造函数。
  * `allowHalfOpen` {boolean} 如果设为 `false`，则当可读端结束时，可写端也会自动结束。
     默认为 `true`。
  * `readableObjectMode` {boolean} 设置流的可读端为 `objectMode`。
     如果 `objectMode` 为 `true`，则不起作用。
     默认为 `false`。
  * `writableObjectMode` {boolean} 设置流的可写端为 `objectMode`。
     如果 `objectMode` 为 `true`，则不起作用。
     默认为 `false`。
  * `readableHighWaterMark` {number} 设置流的可读端的 `highWaterMark`。
     如果已经设置了 `highWaterMark`，则不起作用。
  * `writableHighWaterMark` {number} 设置流的可写端的 `highWaterMark`。
     如果已经设置了 `highWaterMark`，则不起作用。
    
<!-- eslint-disable no-useless-constructor -->
```js
const { Duplex } = require('stream');

class MyDuplex extends Duplex {
  constructor(options) {
    super(options);
    // ...
  }
}
```

使用 ES6 之前的语法：

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

使用简化的构造函数：

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

