<!-- YAML
added:
  - v14.8.0
  - v12.19.0
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/36782
    description: Added optional thisArg.
-->

* `fn` {Function} The function to bind to the current `AsyncResource`.
* `thisArg` {any}

Binds the given function to execute to this `AsyncResource`'s scope.

The returned function will have an `asyncResource` property referencing
the `AsyncResource` to which the function is bound.

