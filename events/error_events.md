
When an error occurs within an `EventEmitter` instance, the typical action is
for an `'error'` event to be emitted. These are treated as special cases
within Node.js.

If an `EventEmitter` does _not_ have at least one listener registered for the
`'error'` event, and an `'error'` event is emitted, the error is thrown, a
stack trace is printed, and the Node.js process exits.

```js
const myEmitter = new MyEmitter();
myEmitter.emit('error', new Error('whoops!'));
// Throws and crashes Node.js
```

To guard against crashing the Node.js process, a listener can be registered
on the [`process` object's `uncaughtException` event][] or the [`domain`][] module
can be used. (_Note, however, that the `domain` module has been deprecated_)

```js
const myEmitter = new MyEmitter();

process.on('uncaughtException', (err) => {
  console.log('whoops! there was an error');
});

myEmitter.emit('error', new Error('whoops!'));
// Prints: whoops! there was an error
```

As a best practice, listeners should always be added for the `'error'` events.

```js
const myEmitter = new MyEmitter();
myEmitter.on('error', (err) => {
  console.log('whoops! there was an error');
});
myEmitter.emit('error', new Error('whoops!'));
// Prints: whoops! there was an error
```

