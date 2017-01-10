
It is recommended that errors occurring during the processing of the
`readable._read()` method are emitted using the `'error'` event rather than
being thrown. Throwing an Error from within `readable._read()` can result in
expected and inconsistent behavior depending on whether the stream is operating
in flowing or paused mode. Using the `'error'` event ensures consistent and
predictable handling of errors.

```js
const Readable = require('stream').Readable;

const myReadable = new Readable({
  read(size) {
    if (checkSomeErrorCondition()) {
      process.nextTick(() => this.emit('error', err));
      return;
    }
    // do some work
  }
});
```

