
* `options` {Object}
  * `highWaterMark` {number} The maximum number of bytes to store in
    the internal buffer before ceasing to read from the underlying
    resource. Defaults to `16384` (16kb), or `16` for `objectMode` streams
  * `encoding` {string} If specified, then buffers will be decoded to
    strings using the specified encoding. Defaults to `null`
  * `objectMode` {boolean} Whether this stream should behave
    as a stream of objects. Meaning that [`stream.read(n)`][stream-read] returns
    a single value instead of a Buffer of size n. Defaults to `false`
  * `read` {Function} Implementation for the [`stream._read()`][stream-_read]
    method.
  * `destroy` {Function} Implementation for the [`stream._destroy()`][readable-_destroy]
    method.

For example:

```js
const { Readable } = require('stream');

class MyReadable extends Readable {
  constructor(options) {
    // Calls the stream.Readable(options) constructor
    super(options);
    // ...
  }
}
```

Or, when using pre-ES6 style constructors:

```js
const { Readable } = require('stream');
const util = require('util');

function MyReadable(options) {
  if (!(this instanceof MyReadable))
    return new MyReadable(options);
  Readable.call(this, options);
}
util.inherits(MyReadable, Readable);
```

Or, using the Simplified Constructor approach:

```js
const { Readable } = require('stream');

const myReadable = new Readable({
  read(size) {
    // ...
  }
});
```

