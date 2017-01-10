<!-- YAML
added: v0.5.1
-->

* `id` {String}
* Returns: {Object} `module.exports` from the resolved module

The `module.require` method provides a way to load a module as if
`require()` was called from the original module.

Note that in order to do this, you must get a reference to the `module`
object.  Since `require()` returns the `module.exports`, and the `module` is
typically *only* available within a specific module's code, it must be
explicitly exported in order to be used.

[`Error`]: errors.html#errors_class_error
[module resolution]: #modules_all_together
