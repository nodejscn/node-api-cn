
解码 buffer 是一个常见的任务，例如使用转换流处理字符串输入。
当使用多字节的字符编码（比如 UTF-8）时，这是一个重要的处理。
下面的例子展示了如何使用 `StringDecoder` 和 [`Writable`] 解码多字节的字符串。

```js
const { Writable } = require('stream');
const { StringDecoder } = require('string_decoder');

class StringWritable extends Writable {
  constructor(options) {
    super(options);
    this._decoder = new StringDecoder(options && options.defaultEncoding);
    this.data = '';
  }
  _write(chunk, encoding, callback) {
    if (encoding === 'buffer') {
      chunk = this._decoder.write(chunk);
    }
    this.data += chunk;
    callback();
  }
  _final(callback) {
    this.data += this._decoder.end();
    callback();
  }
}

const euro = [[0xE2, 0x82], [0xAC]].map(Buffer.from);
const w = new StringWritable();

w.write('货币: ');
w.write(euro[0]);
w.end(euro[1]);

console.log(w.data); // 货币: €
```

