
While using the `inspector` module, an attempt was made to activate the
inspector when it already started to listen on a port. Use `inspector.close()`
before activating it on a different address.

<a id="ERR_INSPECTOR_ALREADY_CONNECTED"></a>
