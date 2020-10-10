<!-- YAML
added:
 - v14.6.0
-->

* `instance` {WebAssembly.Instance}

Attempt to initialize `instance` as a WASI reactor by invoking its
`_initialize()` export, if it is present. If `instance` contains a `_start()`
export, then an exception is thrown.

`initialize()` requires that `instance` exports a [`WebAssembly.Memory`][] named
`memory`. If `instance` does not have a `memory` export an exception is thrown.

If `initialize()` is called more than once, an exception is thrown.

