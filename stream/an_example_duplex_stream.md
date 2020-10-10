
下面举例说明了一个双工流的简单示例，它封装了一个可以写入数据的假设的底层源对象，并且可以从中读取数据，尽管使用的是与 Node.js 流不兼容的 API。 
下面举例了一个双工流的简单示例，它通过可读流接口读回可写流接口的 buffer 传入的写入数据。

```js
const { Duplex } = require('stream');
const kSource = Symbol('source');

class MyDuplex extends Duplex {
  constructor(source, options) {
    super(options);
    this[kSource] = source;
  }

  _write(chunk, encoding, callback) {
    // 底层资源只处理字符串。
    if (Buffer.isBuffer(chunk))
      chunk = chunk.toString();
    this[kSource].writeSomeData(chunk);
    callback();
  }

  _read(size) {
    this[kSource].fetchSomeData(size, (data, encoding) => {
      this.push(Buffer.from(data, encoding));
    });
  }
}
```

双工流最重要的方面是，可读端和可写端相互独立于彼此地共存在同一个对象实例中。

