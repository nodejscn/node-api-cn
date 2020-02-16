<!-- YAML
added: v12.16.0
-->

* `exportNames` {string[]} Array of names that will be exported from the module.
* `evaluateCallback` {Function} Called when the module is evaluated.
* `options`
  * `identifier` {string} String used in stack traces.
   **Default:** `'vm:module(i)'` where `i` is a context-specific ascending
    index.
  * `context` {Object} The [contextified][] object as returned by the
    `vm.createContext()` method, to compile and evaluate this `Module` in.

Creates a new `SyntheticModule` instance.

Objects assigned to the exports of this instance may allow importers of
the module to access information outside the specified `context`. Use
`vm.runInContext()` to create objects in a specific context.

