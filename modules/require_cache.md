<!-- YAML
added: v0.3.0
-->

* {Object}

Modules are cached in this object when they are required. By deleting a key
value from this object, the next `require` will reload the module. Note that
this does not apply to [native addons][], for which reloading will result in an
Error.

