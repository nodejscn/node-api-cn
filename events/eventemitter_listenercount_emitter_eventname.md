<!-- YAML
added: v0.9.12
deprecated: v3.2.0
-->

> Stability: 0 - Deprecated: Use [`emitter.listenerCount()`][] instead.

* `emitter` {EventEmitter} The emitter to query
* `eventName` {string|symbol} The event name

A class method that returns the number of listeners for the given `eventName`
registered on the given `emitter`.

```js
const myEmitter = new EventEmitter();
myEmitter.on('event', () => {});
myEmitter.on('event', () => {});
console.log(EventEmitter.listenerCount(myEmitter, 'event'));
// Prints: 2
```

