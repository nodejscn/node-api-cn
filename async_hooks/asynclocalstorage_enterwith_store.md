<!-- YAML
added:
 - v13.11.0
 - v12.17.0
-->

* `store` {any}

Transitions into the context for the remainder of the current
synchronous execution and then persists the store through any following
asynchronous calls.

Example:

```js
const store = { id: 1 };
// Replaces previous store with the given store object
asyncLocalStorage.enterWith(store);
asyncLocalStorage.getStore(); // Returns the store object
someAsyncOperation(() => {
  asyncLocalStorage.getStore(); // Returns the same object
});
```

This transition will continue for the _entire_ synchronous execution.
This means that if, for example, the context is entered within an event
handler subsequent event handlers will also run within that context unless
specifically bound to another context with an `AsyncResource`. That is why
`run()` should be preferred over `enterWith()` unless there are strong reasons
to use the latter method.

```js
const store = { id: 1 };

emitter.on('my-event', () => {
  asyncLocalStorage.enterWith(store);
});
emitter.on('my-event', () => {
  asyncLocalStorage.getStore(); // Returns the same object
});

asyncLocalStorage.getStore(); // Returns undefined
emitter.emit('my-event');
asyncLocalStorage.getStore(); // Returns the same object
```

