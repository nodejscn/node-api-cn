<!-- YAML
added: v2.0.0
deprecated: v3.0.0
-->

> Stability: 0 - Deprecated: Use `NODE_REPL_HISTORY` instead.

Previously in Node.js/io.js v2.x, REPL history was controlled by using a
`NODE_REPL_HISTORY_FILE` environment variable, and the history was saved in JSON
format. This variable has now been deprecated, and the old JSON REPL history
file will be automatically converted to a simplified plain text format. This new
file will be saved to either the user's home directory, or a directory defined
by the `NODE_REPL_HISTORY` variable, as documented in the
[Environment Variable Options](#repl_environment_variable_options).

