<!-- YAML
added: v0.9.12
deprecated: v4.0.0
-->

> Stability: 0 - Deprecated: Use [`emitter.listenerCount()`][] instead.

A class method that returns the number of listeners for the given `eventName`
registered on the given `emitter`.

```js
const myEmitter = new MyEmitter();
myEmitter.on('event', () => {});
myEmitter.on('event', () => {});
console.log(EventEmitter.listenerCount(myEmitter, 'event'));
// Prints: 2
```

