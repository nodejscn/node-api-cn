
In the scenario of writing to a writable stream from an async iterator,
it is important to ensure the correct handling of backpressure and errors.

```js
const { once } = require('events');

const writable = fs.createWriteStream('./file');

(async function() {
  for await (const chunk of iterator) {
    // Handle backpressure on write().
    if (!writable.write(chunk))
      await once(writable, 'drain');
  }
  writable.end();
  // Ensure completion without errors.
  await once(writable, 'finish');
})();
```

In the above, errors on the write stream would be caught and thrown by the two
`once()` listeners, since `once()` will also handle `'error'` events.

Alternatively the readable stream could be wrapped with `Readable.from()` and
then piped via `.pipe()`:

```js
const { once } = require('events');

const writable = fs.createWriteStream('./file');

(async function() {
  const readable = Readable.from(iterator);
  readable.pipe(writable);
  // Ensure completion without errors.
  await once(writable, 'finish');
})();
```

<!--type=misc-->

