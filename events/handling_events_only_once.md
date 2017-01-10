
When a listener is registered using the `eventEmitter.on()` method, that
listener will be invoked _every time_ the named event is emitted.

```js
const myEmitter = new MyEmitter();
var m = 0;
myEmitter.on('event', () => {
  console.log(++m);
});
myEmitter.emit('event');
// Prints: 1
myEmitter.emit('event');
// Prints: 2
```

Using the `eventEmitter.once()` method, it is possible to register a listener
that is called at most once for a particular event. Once the event is emitted,
the listener is unregistered and *then* called.

```js
const myEmitter = new MyEmitter();
var m = 0;
myEmitter.once('event', () => {
  console.log(++m);
});
myEmitter.emit('event');
// Prints: 1
myEmitter.emit('event');
// Ignored
```

