<!-- YAML
added: v12.3.0
-->

* `iterable` {Iterable} Object implementing the `Symbol.asyncIterator` or
  `Symbol.iterator` iterable protocol.
* `options` {Object} Options provided to `new stream.Readable([options])`.
  By default, `Readable.from()` will set `options.objectMode` to `true`, unless
  this is explicitly opted out by setting `options.objectMode` to `false`.
* Returns: {stream.Readable}

A utility method for creating Readable Streams out of iterators.

```js
const { Readable } = require('stream');

async function * generate() {
  yield 'hello';
  yield 'streams';
}

const readable = Readable.from(generate());

readable.on('data', (chunk) => {
  console.log(chunk);
});
```

