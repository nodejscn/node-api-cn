
Various behaviors of the Node.js REPL can be customized using the following
environment variables:

 - `NODE_REPL_HISTORY` - When a valid path is given, persistent REPL history
   will be saved to the specified file rather than `.node_repl_history` in the
   user's home directory. Setting this value to `""` will disable persistent
   REPL history. Whitespace will be trimmed from the value.
 - `NODE_REPL_HISTORY_SIZE` - Defaults to `1000`. Controls how many lines of
   history will be persisted if history is available. Must be a positive number.
 - `NODE_REPL_MODE` - May be any of `sloppy`, `strict`, or `magic`. Defaults
   to `magic`, which will automatically run "strict mode only" statements in
   strict mode.

