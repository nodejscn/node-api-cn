<!-- YAML
added: v0.11.3
-->

* `path` {string} Default value for `options.path`.
* `options` {Object} See [`tls.connect()`][].
* `callback` {Function} See [`tls.connect()`][].

Same as [`tls.connect()`][] except that `path` can be provided
as an argument instead of an option.

*Note*: A path option, if specified, will take precedence over the path
argument.

