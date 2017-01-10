
<!--type=misc-->

In versions of Node.js prior to v0.10, the Readable stream interface was
simpler, but also less powerful and less useful.

* Rather than waiting for calls the [`stream.read()`][stream-read] method,
  [`'data'`][] events would begin emitting immediately. Applications that
  would need to perform some amount of work to decide how to handle data
  were required to store read data into buffers so the data would not be lost.
* The [`stream.pause()`][stream-pause] method was advisory, rather than
  guaranteed. This meant that it was still necessary to be prepared to receive
  [`'data'`][] events *even when the stream was in a paused state*.

In Node.js v0.10, the [Readable][] class was added. For backwards compatibility
with older Node.js programs, Readable streams switch into "flowing mode" when a
[`'data'`][] event handler is added, or when the
[`stream.resume()`][stream-resume] method is called. The effect is that, even
when not using the new [`stream.read()`][stream-read] method and
[`'readable'`][] event, it is no longer necessary to worry about losing
[`'data'`][] chunks.

While most applications will continue to function normally, this introduces an
edge case in the following conditions:

* No [`'data'`][] event listener is added.
* The [`stream.resume()`][stream-resume] method is never called.
* The stream is not piped to any writable destination.

For example, consider the following code:

```js
// WARNING!  BROKEN!
net.createServer((socket) => {

  // we add an 'end' method, but never consume the data
  socket.on('end', () => {
    // It will never get here.
    socket.end('The message was received but was not processed.\n');
  });

}).listen(1337);
```

In versions of Node.js prior to v0.10, the incoming message data would be
simply discarded. However, in Node.js v0.10 and beyond, the socket remains
paused forever.

The workaround in this situation is to call the
[`stream.resume()`][stream-resume] method to begin the flow of data:

```js
// Workaround
net.createServer((socket) => {

  socket.on('end', () => {
    socket.end('The message was received but was not processed.\n');
  });

  // start the flow of data, discarding it.
  socket.resume();

}).listen(1337);
```

In addition to new Readable streams switching into flowing mode,
pre-v0.10 style streams can be wrapped in a Readable class using the
[`readable.wrap()`][`stream.wrap()`] method.


