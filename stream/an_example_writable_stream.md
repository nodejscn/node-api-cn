下面说明了一个相当简单（有点无意义）的可写流实现。虽然这个具体的可写流实例没有任何真正的特殊用途，但该示例说明了一个自定义流实例所需要的元素：

```js
const { Writable } = require('stream');

class MyWritable extends Writable {
  constructor(options) {
    super(options);
    // ...
  }

  _write(chunk, encoding, callback) {
    if (chunk.toString().indexOf('a') >= 0) {
      callback(new Error('chunk is invalid'));
    } else {
      callback();
    }
  }
}
```



