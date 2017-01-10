<!-- YAML
added: v0.1.26
-->

* `eventName` {String|Symbol} The name of the event being listened for
* `listener` {Function} The event handler function

The `EventEmitter` instance will emit its own `'newListener'` event *before*
a listener is added to its internal array of listeners.

Listeners registered for the `'newListener'` event will be passed the event
name and a reference to the listener being added.

The fact that the event is triggered before adding the listener has a subtle
but important side effect: any *additional* listeners registered to the same
`name` *within* the `'newListener'` callback will be inserted *before* the
listener that is in the process of being added.

```js
const myEmitter = new MyEmitter();
// Only do this once so we don't loop forever
myEmitter.once('newListener', (event, listener) => {
  if (event === 'event') {
    // Insert a new listener in front
    myEmitter.on('event', () => {
      console.log('B');
    });
  }
});
myEmitter.on('event', () => {
  console.log('A');
});
myEmitter.emit('event');
// Prints:
//   B
//   A
```

