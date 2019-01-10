<!-- YAML
added: v1.2.0
-->

对于简单的案例，构造流可以不依赖继承。
直接创建 `stream.Writable`、`stream.Readable`、`stream.Duplex` 或 `stream.Transform` 的实例，并传入对应的方法作为构造函数选项。

```js
const { Writable } = require('stream');

const myWritable = new Writable({
  write(chunk, encoding, callback) {
    // ...
  }
});
```

