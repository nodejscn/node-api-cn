
> Stability: 0 - Deprecated.  Please recover from failed IO actions
> explicitly via error event handlers set on the domain.

Once `dispose` has been called, the domain will no longer be used by callbacks
bound into the domain via `run`, `bind`, or `intercept`, and a `'dispose'` event
is emitted.

[`domain.add(emitter)`]: #domain_domain_add_emitter
[`domain.bind(callback)`]: #domain_domain_bind_callback
[`domain.dispose()`]: #domain_domain_dispose
[`domain.exit()`]: #domain_domain_exit
[`Error`]: errors.html#errors_class_error
[`EventEmitter`]: events.html#events_class_eventemitter
[`setInterval()`]: timers.html#timers_setinterval_callback_delay_args
[`setTimeout()`]: timers.html#timers_settimeout_callback_delay_args
[`throw`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw
