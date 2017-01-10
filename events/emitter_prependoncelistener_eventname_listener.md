<!-- YAML
added: v6.0.0
-->

* `eventName` {String|Symbol} The name of the event.
* `listener` {Function} The callback function

Adds a **one time** `listener` function for the event named `eventName` to the
*beginning* of the listeners array. The next time `eventName` is triggered, this
listener is removed, and then invoked.

```js
server.prependOnceListener('connection', (stream) => {
  console.log('Ah, we have our first user!');
});
```

Returns a reference to the `EventEmitter`, so that calls can be chained.

