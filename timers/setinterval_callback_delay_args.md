<!-- YAML
added: v0.0.1
-->

* `callback` {Function} The function to call when the timer elapses.
* `delay` {number} The number of milliseconds to wait before calling the
  `callback`.
* `...args` {any} Optional arguments to pass when the `callback` is called.

Schedules repeated execution of `callback` every `delay` milliseconds.
Returns a `Timeout` for use with [`clearInterval()`][].

When `delay` is larger than `2147483647` or less than `1`, the `delay` will be
set to `1`.

If `callback` is not a function, a [`TypeError`][] will be thrown.

