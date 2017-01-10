<!-- YAML
added: v0.9.4
-->

* Returns: `this`

The `readable.resume()` method causes an explicitly paused Readable stream to
resume emitting [`'data'`][] events, switching the stream into flowing mode.

The `readable.resume()` method can be used to fully consume the data from a
stream without actually processing any of that data as illustrated in the
following example:

```js
getReadableStreamSomehow()
  .resume()
  .on('end', () => {
    console.log('Reached the end, but did not read anything.');
  });
```

