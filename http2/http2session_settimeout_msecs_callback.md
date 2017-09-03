<!-- YAML
added: v8.4.0
-->

* `msecs` {number}
* `callback` {Function}
* Returns: {undefined}

Used to set a callback function that is called when there is no activity on
the `Http2Session` after `msecs` milliseconds. The given `callback` is
registered as a listener on the `'timeout'` event.

