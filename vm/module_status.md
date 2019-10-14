
* {string}

The current status of the module. Will be one of:

* `'unlinked'`: `module.link()` has not yet been called.

* `'linking'`: `module.link()` has been called, but not all Promises returned
  by the linker function have been resolved yet.

* `'linked'`: The module has been linked successfully, and all of its
  dependencies are linked, but `module.evaluate()` has not yet been called.

* `'evaluating'`: The module is being evaluated through a `module.evaluate()` on
  itself or a parent module.

* `'evaluated'`: The module has been successfully evaluated.

* `'errored'`: The module has been evaluated, but an exception was thrown.

Other than `'errored'`, this status string corresponds to the specification's
[Source Text Module Record][]'s `[[Status]]` field. `'errored'` corresponds to
`'evaluated'` in the specification, but with `[[EvaluationError]]` set to a
value that is not `undefined`.

