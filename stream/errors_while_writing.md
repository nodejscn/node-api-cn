
It is recommended that errors occurring during the processing of the
`writable._write()` and `writable._writev()` methods are reported by invoking
the callback and passing the error as the first argument. This will cause an
`'error'` event to be emitted by the Writable. Throwing an Error from within
`writable._write()` can result in unexpected and inconsistent behavior depending
on how the stream is being used.  Using the callback ensures consistent and
predictable handling of errors.

```js
const { Writable } = require('stream');

const myWritable = new Writable({
  write(chunk, encoding, callback) {
    if (chunk.toString().indexOf('a') >= 0) {
      callback(new Error('chunk is invalid'));
    } else {
      callback();
    }
  }
});
```

