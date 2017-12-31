
* `options` {Object} 传给可读和可写构造函数。
  还有如下字段:
  * `transform` {Function} 对[`stream._transform()`][stream-_transform]方法的实现。
  * `flush` {Function} 对[`stream._flush()`][stream-_flush]方法的实现。

例如:

```js
const { Transform } = require('stream');

class MyTransform extends Transform {
  constructor(options) {
    super(options);
    // ...
  }
}
```

或者，用ES6构造方法:

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

又或者, 用简化构造方法:

```js
const { Transform } = require('stream');

const myTransform = new Transform({
  transform(chunk, encoding, callback) {
    // ...
  }
});
```

