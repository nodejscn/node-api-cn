
<!--type=example-->

The following is a basic example of a Readable stream that emits the numerals
from 1 to 1,000,000 in ascending order, and then ends.

```js
const Readable = require('stream').Readable;

class Counter extends Readable {
  constructor(opt) {
    super(opt);
    this._max = 1000000;
    this._index = 1;
  }

  _read() {
    var i = this._index++;
    if (i > this._max)
      this.push(null);
    else {
      var str = '' + i;
      var buf = Buffer.from(str, 'ascii');
      this.push(buf);
    }
  }
}
```

