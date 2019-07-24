
* `options` {Object} 同时传给 `Writable` 和 `Readable` 的构造函数。
  * `transform` {Function} 对 [`stream._transform()`][stream-_transform] 的实现。
  * `flush` {Function} 对 [`stream._flush()`][stream-_flush] 的实现。

<!-- eslint-disable no-useless-constructor -->
```js
const { Transform } = require('stream');

class MyTransform extends Transform {
  constructor(options) {
    super(options);
    // ...
  }
}
```

使用 ES6 之前的语法：

```js
const { Transform } = require('stream');
const util = require('util');

function MyTransform(options) {
  if (!(this instanceof MyTransform))
    return new MyTransform(options);
  Transform.call(this, options);
}
util.inherits(MyTransform, Transform);
```

使用简化的构造函数：

```js
const { Transform } = require('stream');

const myTransform = new Transform({
  transform(chunk, encoding, callback) {
    // ...
  }
});
```

