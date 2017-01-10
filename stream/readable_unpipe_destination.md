<!-- YAML
added: v0.9.4
-->

* `destination` {stream.Writable} Optional specific stream to unpipe

The `readable.unpipe()` method detaches a Writable stream previously attached
using the [`stream.pipe()`][] method.

If the `destination` is not specified, then *all* pipes are detached.

If the `destination` is specified, but no pipe is set up for it, then
the method does nothing.

```js
const readable = getReadableStreamSomehow();
const writable = fs.createWriteStream('file.txt');
// All the data from readable goes into 'file.txt',
// but only for the first second
readable.pipe(writable);
setTimeout(() => {
  console.log('Stop writing to file.txt');
  readable.unpipe(writable);
  console.log('Manually close the file stream');
  writable.end();
}, 1000);
```

