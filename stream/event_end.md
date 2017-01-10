<!-- YAML
added: v0.9.4
-->

The `'end'` event is emitted when there is no more data to be consumed from
the stream.

*Note*: The `'end'` event **will not be emitted** unless the data is
completely consumed. This can be accomplished by switching the stream into
flowing mode, or by calling [`stream.read()`][stream-read] repeatedly until
all data has been consumed.

```js
const readable = getReadableStreamSomehow();
readable.on('data', (chunk) => {
  console.log(`Received ${chunk.length} bytes of data.`);
});
readable.on('end', () => {
  console.log('There will be no more data.');
});
```

