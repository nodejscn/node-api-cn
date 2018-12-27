<!-- YAML
added: v0.11.3
-->

* `port` {number} Default value for `options.port`.
* `host` {string} Default value for `options.host`.
* `options` {Object} See [`tls.connect()`][].
* `callback` {Function} See [`tls.connect()`][].
* Returns: {tls.TLSSocket}

Same as [`tls.connect()`][] except that `port` and `host` can be provided
as arguments instead of options.

A port or host option, if specified, will take precedence over any port or host
argument.

