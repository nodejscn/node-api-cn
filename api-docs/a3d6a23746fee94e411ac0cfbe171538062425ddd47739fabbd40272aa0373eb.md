
下面的例子是一个简单的可写流的实现。

```js
const { Writable } = require('stream');

class MyWritable extends Writable {
  constructor(options) {
    super(options);
    // ...
  }

  _write(chunk, encoding, callback) {
    if (chunk.toString().indexOf('a') >= 0) {
      callback(new Error('无效的数据块'));
    } else {
      callback();
    }
  }
}
```

