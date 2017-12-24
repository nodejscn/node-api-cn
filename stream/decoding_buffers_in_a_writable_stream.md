
Decoding buffers is a common task, for instance, when using transformers whose
input is a string. This is not a trivial process when using multi-byte
characters encoding, such as UTF-8. The following example shows how to decode
multi-byte strings using `StringDecoder` and [Writable][].

```js
const { Writable } = require('stream');
const { StringDecoder } = require('string_decoder');

class StringWritable extends Writable {
  constructor(options) {
    super(options);
    const state = this._writableState;
    this._decoder = new StringDecoder(state.defaultEncoding);
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

w.write('currency: ');
w.write(euro[0]);
w.end(euro[1]);

console.log(w.data); // currency: €
```

