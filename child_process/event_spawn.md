<!-- YAML
added: v15.1.0
-->

The `'spawn'` event is emitted once the child process has spawned successfully.
If the child process does not spawn successfully, the `'spawn'` event is not
emitted and the `'error'` event is emitted instead.

If emitted, the `'spawn'` event comes before all other events and before any
data is received via `stdout` or `stderr`.

The `'spawn'` event will fire regardless of whether an error occurs **within**
the spawned process. For example, if `bash some-command` spawns successfully,
the `'spawn'` event will fire, though `bash` may fail to spawn `some-command`.
This caveat also applies when using `{ shell: true }`.

