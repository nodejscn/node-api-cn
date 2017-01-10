<!-- YAML
added: v0.11.2
-->

By default, a maximum of `10` listeners can be registered for any single
event. This limit can be changed for individual `EventEmitter` instances
using the [`emitter.setMaxListeners(n)`][] method. To change the default
for *all* `EventEmitter` instances, the `EventEmitter.defaultMaxListeners`
property can be used.

Take caution when setting the `EventEmitter.defaultMaxListeners` because the
change effects *all* `EventEmitter` instances, including those created before
the change is made. However, calling [`emitter.setMaxListeners(n)`][] still has
precedence over `EventEmitter.defaultMaxListeners`.

Note that this is not a hard limit. The `EventEmitter` instance will allow
more listeners to be added but will output a trace warning to stderr indicating
that a "possible EventEmitter memory leak" has been detected. For any single
`EventEmitter`, the `emitter.getMaxListeners()` and `emitter.setMaxListeners()`
methods can be used to temporarily avoid this warning:

```js
emitter.setMaxListeners(emitter.getMaxListeners() + 1);
emitter.once('event', () => {
  // do stuff
  emitter.setMaxListeners(Math.max(emitter.getMaxListeners() - 1, 0));
});
```

The [`--trace-warnings`][] command line flag can be used to display the
stack trace for such warnings.

The emitted warning can be inspected with [`process.on('warning')`][] and will
have the additional `emitter`, `type` and `count` properties, referring to
the event emitter instance, the event’s name and the number of attached
listeners, respectively.

