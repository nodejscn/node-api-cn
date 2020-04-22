<!-- YAML
added: v13.7.0
-->

* `path` {string}
* `error` {Error}
* Returns: {module.SourceMap}

`path` is the resolved path for the file for which a corresponding source map
should be fetched.

The `error` instance should be passed as the second parameter to `findSourceMap`
in exceptional flows, e.g., when an overridden
[`Error.prepareStackTrace(error, trace)`][] is invoked. Modules are not added to
the module cache until they are successfully loaded, in these cases source maps
will be associated with the `error` instance along with the `path`.

