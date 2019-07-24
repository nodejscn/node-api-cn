<!-- YAML
added: v10.0.0
-->

> Stability: 1 - Experimental

* Returns: {AsyncIterator} to fully consume the stream.

```js
const fs = require('fs');

async function print(readable) {
  readable.setEncoding('utf8');
  let data = '';
  for await (const k of readable) {
    data += k;
  }
  console.log(data);
}

print(fs.createReadStream('file')).catch(console.log);
```

If the loop terminates with a `break` or a `throw`, the stream will be
destroyed. In other terms, iterating over a stream will consume the stream
fully. The stream will be read in chunks of size equal to the `highWaterMark`
option. In the code example above, data will be in a single chunk if the file
has less then 64kb of data because no `highWaterMark` option is provided to
[`fs.createReadStream()`][].

