<!-- YAML
added: v0.9.4
-->

* `size` {Number} Optional argument to specify how much data to read.
* Return {String|Buffer|Null}

The `readable.read()` method pulls some data out of the internal buffer and
returns it. If no data available to be read, `null` is returned. By default,
the data will be returned as a `Buffer` object unless an encoding has been
specified using the `readable.setEncoding()` method or the stream is operating
in object mode.

The optional `size` argument specifies a specific number of bytes to read. If
`size` bytes are not available to be read, `null` will be returned *unless*
the stream has ended, in which case all of the data remaining in the internal
buffer will be returned (*even if it exceeds `size` bytes*).

If the `size` argument is not specified, all of the data contained in the
internal buffer will be returned.

The `readable.read()` method should only be called on Readable streams operating
in paused mode. In flowing mode, `readable.read()` is called automatically until
the internal buffer is fully drained.

```js
const readable = getReadableStreamSomehow();
readable.on('readable', () => {
  var chunk;
  while (null !== (chunk = readable.read())) {
    console.log(`Received ${chunk.length} bytes of data.`);
  }
});
```

In general, it is recommended that developers avoid the use of the `'readable'`
event and the `readable.read()` method in favor of using either
`readable.pipe()` or the `'data'` event.

A Readable stream in object mode will always return a single item from
a call to [`readable.read(size)`][stream-read], regardless of the value of the
`size` argument.

*Note:* If the `readable.read()` method returns a chunk of data, a `'data'`
event will also be emitted.

*Note*: Calling [`stream.read([size])`][stream-read] after the [`'end'`][]
event has been emitted will return `null`. No runtime error will be raised.

