
下面是一个可读可写流包装了一个假定的可读可写的底层源对象，
尽管用了一个与Node.js流不兼容的API。

下面是一个简单的例子，
在一个可读可写流中，来的buffers通过[Writable][] 接口写入数据，再通过[Readable][]接口读回数据。


```js
const { Duplex } = require('stream');
const kSource = Symbol('source');

class MyDuplex extends Duplex {
  constructor(source, options) {
    super(options);
    this[kSource] = source;
  }

  _write(chunk, encoding, callback) {
    // The underlying source only deals with strings
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

尽管在一个对象实例中共存，读端和写端却是相互独立于彼此，这是可读可写流最为重要的一点。
