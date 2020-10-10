<!-- YAML
added:
 - v13.7.0
 - v12.17.0
-->

* `path` {string}
* `error` {Error}
* Returns: {module.SourceMap}

`path` is the resolved path for the file for which a corresponding source map
should be fetched.

The `error` instance should be passed as the second parameter to `findSourceMap`
in exceptional flows, such as when an overridden
[`Error.prepareStackTrace(error, trace)`][] is invoked. Modules are not added to
the module cache until they are successfully loaded. In these cases, source maps
are associated with the `error` instance along with the `path`.

