<!-- YAML
added:
 - v13.3.0
 - v12.16.0
-->

* `instance` {WebAssembly.Instance}

Attempt to begin execution of `instance` by invoking its `_start()` export.
If `instance` does not contain a `_start()` export, then `start()` attempts to
invoke the `__wasi_unstable_reactor_start()` export. If neither of those exports
is present on `instance`, then `start()` does nothing.

`start()` requires that `instance` exports a [`WebAssembly.Memory`][] named
`memory`. If `instance` does not have a `memory` export an exception is thrown.

