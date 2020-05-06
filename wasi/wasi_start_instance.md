<!-- YAML
added:
 - v13.3.0
 - v12.16.0
-->

* `instance` {WebAssembly.Instance}

Attempt to begin execution of `instance` as a WASI command by invoking its
`_start()` export. If `instance` does not contain a `_start()` export, or if
`instance` contains an `_initialize()` export, then an exception is thrown.

`start()` requires that `instance` exports a [`WebAssembly.Memory`][] named
`memory`. If `instance` does not have a `memory` export an exception is thrown.

If `start()` is called more than once, an exception is thrown.

