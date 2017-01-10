<!-- YAML
added: v0.9.4
-->

The `'readable'` event is emitted when there is data available to be read from
the stream. In some cases, attaching a listener for the `'readable'` event will
cause some amount of data to be read into an internal buffer.

```javascript
const readable = getReadableStreamSomehow();
readable.on('readable', () => {
  // there is some data to read now
});
```
The `'readable'` event will also be emitted once the end of the stream data
has been reached but before the `'end'` event is emitted.

Effectively, the `'readable'` event indicates that the stream has new
information: either new data is available or the end of the stream has been
reached. In the former case, [`stream.read()`][stream-read] will return the
available data. In the latter case, [`stream.read()`][stream-read] will return
`null`. For instance, in the following example, `foo.txt` is an empty file:

```js
const fs = require('fs');
const rr = fs.createReadStream('foo.txt');
rr.on('readable', () => {
  console.log('readable:', rr.read());
});
rr.on('end', () => {
  console.log('end');
});
```

The output of running this script is:

```txt
$ node test.js
readable: null
end
```

*Note*: In general, the `readable.pipe()` and `'data'` event mechanisms are
preferred over the use of the `'readable'` event.

