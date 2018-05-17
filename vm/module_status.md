
* {string}

The current status of the module. Will be one of:

- `'uninstantiated'`: The module is not instantiated. It may because of any of
  the following reasons:

  - The module was just created.
  - `module.instantiate()` has been called on this module, but it failed for
    some reason.

  This status does not convey any information regarding if `module.link()` has
  been called. See `module.linkingStatus` for that.

- `'instantiating'`: The module is currently being instantiated through a
  `module.instantiate()` call on itself or a parent module.

- `'instantiated'`: The module has been instantiated successfully, but
  `module.evaluate()` has not yet been called.

- `'evaluating'`: The module is being evaluated through a `module.evaluate()` on
  itself or a parent module.

- `'evaluated'`: The module has been successfully evaluated.

- `'errored'`: The module has been evaluated, but an exception was thrown.

Other than `'errored'`, this status string corresponds to the specification's
[Source Text Module Record][]'s `[[Status]]` field. `'errored'` corresponds to
`'evaluated'` in the specification, but with `[[EvaluationError]]` set to a
value that is not `undefined`.

