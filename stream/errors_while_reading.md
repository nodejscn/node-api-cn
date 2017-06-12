
It is recommended that errors occurring during the processing of the
`readable._read()` method are emitted using the `'error'` event rather than
being thrown. Throwing an Error from within `readable._read()` can result in
unexpected and inconsistent behavior depending on whether the stream is
operating in flowing or paused mode. Using the `'error'` event ensures
consistent and predictable handling of errors.

<!-- eslint-disable no-useless-return -->
```js
const { Readable } = require('stream');

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

