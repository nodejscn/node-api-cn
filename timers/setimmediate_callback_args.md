<!-- YAML
added: v0.9.1
-->

* `callback` {Function} The function to call at the end of this turn of
  [the Node.js Event Loop]
* `...args` {any} Optional arguments to pass when the `callback` is called.

Schedules the "immediate" execution of the `callback` after I/O events'
callbacks and before timers created using [`setTimeout()`][] and
[`setInterval()`][] are triggered. Returns an `Immediate` for use with
[`clearImmediate()`][].

When multiple calls to `setImmediate()` are made, the `callback` functions are
queued for execution in the order in which they are created. The entire callback
queue is processed every event loop iteration. If an immediate timer is queued
from inside an executing callback, that timer will not be triggered until the
next event loop iteration.

If `callback` is not a function, a [`TypeError`][] will be thrown.

