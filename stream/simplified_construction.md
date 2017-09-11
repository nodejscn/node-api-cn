<!-- YAML
added: v1.2.0
-->

对于许多简单的案例，它是有可能在不依赖继承的情况下创建流。这可以直接创建流实例，通过流基础类`stream.Weiteable`，`stream.Readable`，`stream.Duplex`，或者`stream.Transform`传入对象完成，对象包含合适的方法作为构造函数选项。

```js
const { Writable } = require('stream');

const myWritable = new Writable({
  write(chunk, encoding, callback) {
    // ...
  }
});
```
