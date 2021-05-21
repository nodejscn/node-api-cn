<!-- YAML
added: v16.0.0
-->

* {boolean}

True if the process is a primary. This is determined
by the `process.env.NODE_UNIQUE_ID`. If `process.env.NODE_UNIQUE_ID` is
undefined, then `isPrimary` is `true`.

