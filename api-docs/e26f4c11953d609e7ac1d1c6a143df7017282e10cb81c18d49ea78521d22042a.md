<!-- YAML
added: v0.1.94
-->
* `encoding` {string} The [encoding][] of the return value.
* Returns: {Buffer | string}

Calculates the HMAC digest of all of the data passed using [`hmac.update()`][].
If `encoding` is
provided a string is returned; otherwise a [`Buffer`][] is returned;

The `Hmac` object can not be used again after `hmac.digest()` has been
called. Multiple calls to `hmac.digest()` will result in an error being thrown.

