
以下举例了一个相当简单（并且有点无意义）的自定义的 `Writable` 流的实现。 
虽然这个特定的 `Writable` 流的实例没有任何实际的特殊用途，但该示例说明了一个自定义的 [`Writable`] 流实例的每个必需元素：

```js
const { Writable } = require('stream');

class MyWritable extends Writable {
  _write(chunk, encoding, callback) {
    if (chunk.toString().indexOf('a') >= 0) {
      callback(new Error('数据块是无效的'));
    } else {
      callback();
    }
  }
}
```

