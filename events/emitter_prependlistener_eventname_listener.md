<!-- YAML
added: v6.0.0
-->

* `eventName` {String|Symbol} The name of the event.
* `listener` {Function} The callback function

Adds the `listener` function to the *beginning* of the listeners array for the
event named `eventName`. No checks are made to see if the `listener` has
already been added. Multiple calls passing the same combination of `eventName`
and `listener` will result in the `listener` being added, and called, multiple
times.

```js
server.prependListener('connection', (stream) => {
  console.log('someone connected!');
});
```

Returns a reference to the `EventEmitter`, so that calls can be chained.

