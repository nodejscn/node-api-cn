<!-- YAML
added: v0.0.1
-->

* `callback` {Function} The function to call when the timer elapses.
* `delay` {number} The number of milliseconds to wait before calling the
  `callback`.
* `...args` {any} Optional arguments to pass when the `callback` is called.

Schedules execution of a one-time `callback` after `delay` milliseconds.
Returns a `Timeout` for use with [`clearTimeout()`][].

The `callback` will likely not be invoked in precisely `delay` milliseconds.
Node.js makes no guarantees about the exact timing of when callbacks will fire,
nor of their ordering. The callback will be called as close as possible to the
time specified.

*Note*: When `delay` is larger than `2147483647` or less than `1`, the `delay`
will be set to `1`.

If `callback` is not a function, a [`TypeError`][] will be thrown.

