
* `options` {Object}
  * `highWaterMark` {Number} Buffer level when
    [`stream.write()`][stream-write] starts returning `false`. Defaults to
    `16384` (16kb), or `16` for `objectMode` streams.
  * `decodeStrings` {Boolean} Whether or not to decode strings into
    Buffers before passing them to [`stream._write()`][stream-_write].
    Defaults to `true`
  * `objectMode` {Boolean} Whether or not the
    [`stream.write(anyObj)`][stream-write] is a valid operation. When set,
    it becomes possible to write JavaScript values other than string or
    `Buffer` if supported by the stream implementation. Defaults to `false`
  * `write` {Function} Implementation for the
    [`stream._write()`][stream-_write] method.
  * `writev` {Function} Implementation for the
    [`stream._writev()`][stream-_writev] method.

For example:

```js
const Writable = require('stream').Writable;

class MyWritable extends Writable {
  constructor(options) {
    // Calls the stream.Writable() constructor
    super(options);
  }
}
```

Or, when using pre-ES6 style constructors:

```js
const Writable = require('stream').Writable;
const util = require('util');

function MyWritable(options) {
  if (!(this instanceof MyWritable))
    return new MyWritable(options);
  Writable.call(this, options);
}
util.inherits(MyWritable, Writable);
```

Or, using the Simplified Constructor approach:

```js
const Writable = require('stream').Writable;

const myWritable = new Writable({
  write(chunk, encoding, callback) {
    // ...
  },
  writev(chunks, callback) {
    // ...
  }
});
```

