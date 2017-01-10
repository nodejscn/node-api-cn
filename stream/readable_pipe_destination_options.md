<!-- YAML
added: v0.9.4
-->

* `destination` {stream.Writable} The destination for writing data
* `options` {Object} Pipe options
  * `end` {Boolean} End the writer when the reader ends. Defaults to `true`.

The `readable.pipe()` method attaches a [Writable][] stream to the `readable`,
causing it to switch automatically into flowing mode and push all of its data
to the attached [Writable][]. The flow of data will be automatically managed so
that the destination Writable stream is not overwhelmed by a faster Readable
stream.

The following example pipes all of the data from the `readable` into a file
named `file.txt`:

```js
const readable = getReadableStreamSomehow();
const writable = fs.createWriteStream('file.txt');
// All the data from readable goes into 'file.txt'
readable.pipe(writable);
```
It is possible to attach multiple Writable streams to a single Readable stream.

The `readable.pipe()` method returns a reference to the *destination* stream
making it possible to set up chains of piped streams:

```js
const r = fs.createReadStream('file.txt');
const z = zlib.createGzip();
const w = fs.createWriteStream('file.txt.gz');
r.pipe(z).pipe(w);
```

By default, [`stream.end()`][stream-end] is called on the destination Writable
stream when the source Readable stream emits [`'end'`][], so that the
destination is no longer writable. To disable this default behavior, the `end`
option can be passed as `false`, causing the destination stream to remain open,
as illustrated in the following example:

```js
reader.pipe(writer, { end: false });
reader.on('end', () => {
  writer.end('Goodbye\n');
});
```

One important caveat is that if the Readable stream emits an error during
processing, the Writable destination *is not closed* automatically. If an
error occurs, it will be necessary to *manually* close each stream in order
to prevent memory leaks.

*Note*: The [`process.stderr`][] and [`process.stdout`][] Writable streams are
never closed until the Node.js process exits, regardless of the specified
options.

