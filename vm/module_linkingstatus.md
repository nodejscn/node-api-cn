
* {string}

The current linking status of `module`. It will be one of the following values:

* `'unlinked'`: `module.link()` has not yet been called.
* `'linking'`: `module.link()` has been called, but not all Promises returned by
  the linker function have been resolved yet.
* `'linked'`: `module.link()` has been called, and all its dependencies have
  been successfully linked.
* `'errored'`: `module.link()` has been called, but at least one of its
  dependencies failed to link, either because the callback returned a `Promise`
  that is rejected, or because the `Module` the callback returned is invalid.

