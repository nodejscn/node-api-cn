
For Duplex streams, `objectMode` can be set exclusively for either the Readable
or Writable side using the `readableObjectMode` and `writableObjectMode` options
respectively.

In the following example, for instance, a new Transform stream (which is a
type of [Duplex][] stream) is created that has an object mode Writable side
that accepts JavaScript numbers that are converted to hexadecimal strings on
the Readable side.

```js
const { Transform } = require('stream');

// All Transform streams are also Duplex Streams
const myTransform = new Transform({
  writableObjectMode: true,

  transform(chunk, encoding, callback) {
    // Coerce the chunk to a number if necessary
    chunk |= 0;

    // Transform the chunk into something else.
    const data = chunk.toString(16);

    // Push the data onto the readable queue.
    callback(null, '0'.repeat(data.length % 2) + data);
  }
});

myTransform.setEncoding('ascii');
myTransform.on('data', (chunk) => console.log(chunk));

myTransform.write(1);
// Prints: 01
myTransform.write(10);
// Prints: 0a
myTransform.write(100);
// Prints: 64
```

