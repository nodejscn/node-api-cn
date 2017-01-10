<!-- YAML
added: v0.1.26
-->

Removes the specified `listener` from the listener array for the event named
`eventName`.

```js
var callback = (stream) => {
  console.log('someone connected!');
};
server.on('connection', callback);
// ...
server.removeListener('connection', callback);
```

`removeListener` will remove, at most, one instance of a listener from the
listener array. If any single listener has been added multiple times to the
listener array for the specified `eventName`, then `removeListener` must be
called multiple times to remove each instance.

Note that once an event has been emitted, all listeners attached to it at the
time of emitting will be called in order. This implies that any `removeListener()`
or `removeAllListeners()` calls *after* emitting and *before* the last listener
finishes execution will not remove them from `emit()` in progress. Subsequent
events will behave as expected.

```js
const myEmitter = new MyEmitter();

var callbackA = () => {
  console.log('A');
  myEmitter.removeListener('event', callbackB);
};

var callbackB = () => {
  console.log('B');
};

myEmitter.on('event', callbackA);

myEmitter.on('event', callbackB);

// callbackA removes listener callbackB but it will still be called.
// Internal listener array at time of emit [callbackA, callbackB]
myEmitter.emit('event');
// Prints:
//   A
//   B

// callbackB is now removed.
// Internal listener array [callbackA]
myEmitter.emit('event');
// Prints:
//   A

```

Because listeners are managed using an internal array, calling this will
change the position indices of any listener registered *after* the listener
being removed. This will not impact the order in which listeners are called,
but it means that any copies of the listener array as returned by
the `emitter.listeners()` method will need to be recreated.

Returns a reference to the `EventEmitter`, so that calls can be chained.

