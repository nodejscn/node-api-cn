<!-- YAML
added: v10.0.0
-->

* `stream` {Stream} A readable and/or writable stream.
* `callback` {Function} A callback function that takes an optional error
  argument.

A function to get notified when a stream is no longer readable, writable
or has experienced an error or a premature close event.

```js
const { finished } = require('stream');

const rs = fs.createReadStream('archive.tar');

finished(rs, (err) => {
  if (err) {
    console.error('Stream failed', err);
  } else {
    console.log('Stream is done reading');
  }
});

rs.resume(); // drain the stream
```

Especially useful in error handling scenarios where a stream is destroyed
prematurely (like an aborted HTTP request), and will not emit `'end'`
or `'finish'`.

The `finished` API is promisify'able as well;

```js
const finished = util.promisify(stream.finished);

const rs = fs.createReadStream('archive.tar');

async function run() {
  await finished(rs);
  console.log('Stream is done reading');
}

run().catch(console.error);
rs.resume(); // drain the stream
```

