
As of Node 8.0.0, the handlers of Promises are run inside the domain in
which the call to `.then` or `.catch` itself was made:

```js
const d1 = domain.create();
const d2 = domain.create();

let p;
d1.run(() => {
  p = Promise.resolve(42);
});

d2.run(() => {
  p.then((v) => {
    // running in d2
  });
});
```

A callback may be bound to a specific domain using [`domain.bind(callback)`][]:

```js
const d1 = domain.create();
const d2 = domain.create();

let p;
d1.run(() => {
  p = Promise.resolve(42);
});

d2.run(() => {
  p.then(p.domain.bind((v) => {
    // running in d1
  }));
});
```

Note that domains will not interfere with the error handling mechanisms for
Promises, i.e. no `error` event will be emitted for unhandled Promise
rejections.

[`Error`]: errors.html#errors_class_error
[`EventEmitter`]: events.html#events_class_eventemitter
[`domain.add(emitter)`]: #domain_domain_add_emitter
[`domain.bind(callback)`]: #domain_domain_bind_callback
[`domain.dispose()`]: #domain_domain_dispose
[`domain.exit()`]: #domain_domain_exit
[`setInterval()`]: timers.html#timers_setinterval_callback_delay_args
[`setTimeout()`]: timers.html#timers_settimeout_callback_delay_args
[`throw`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw
