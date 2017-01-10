
The following illustrates a rather simplistic (and somewhat pointless) custom
Writable stream implementation. While this specific Writable stream instance
is not of any real particular usefulness, the example illustrates each of the
required elements of a custom [Writable][] stream instance:

```js
const Writable = require('stream').Writable;

class MyWritable extends Writable {
  constructor(options) {
    super(options);
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

