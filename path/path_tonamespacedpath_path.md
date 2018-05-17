<!-- YAML
added: v9.0.0
-->

* `path` {string}
* Returns: {string}

On Windows systems only, returns an equivalent [namespace-prefixed path][] for
the given `path`. If `path` is not a string, `path` will be returned without
modifications.

This method is meaningful only on Windows system. On posix systems, the
method is non-operational and always returns `path` without modifications.

