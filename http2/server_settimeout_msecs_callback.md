<!-- YAML
added: v8.4.0
-->

* `msecs` {number} **Default:** `120000` (2 minutes)
* `callback` {Function}
* Returns: {Http2Server}

Used to set the timeout value for http2 server requests,
and sets a callback function that is called when there is no activity
on the `Http2Server` after `msecs` milliseconds.

The given callback is registered as a listener on the `'timeout'` event.

In case of no callback function were assigned, a new `ERR_INVALID_CALLBACK`
error will be thrown.

