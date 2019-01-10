<!-- YAML
added: v10.10.0
-->

* `pid` {integer} The process ID to set scheduling priority for.
  **Default** `0`.
* `priority` {integer} The scheduling priority to assign to the process.

The `os.setPriority()` method attempts to set the scheduling priority for the
process specified by `pid`. If `pid` is not provided, or is `0`, the priority
of the current process is used.

The `priority` input must be an integer between `-20` (high priority) and `19`
(low priority). Due to differences between Unix priority levels and Windows
priority classes, `priority` is mapped to one of six priority constants in
`os.constants.priority`. When retrieving a process priority level, this range
mapping may cause the return value to be slightly different on Windows. To avoid
confusion, it is recommended to set `priority` to one of the priority constants.

On Windows setting priority to `PRIORITY_HIGHEST` requires elevated user,
otherwise the set priority will be silently reduced to `PRIORITY_HIGH`.

