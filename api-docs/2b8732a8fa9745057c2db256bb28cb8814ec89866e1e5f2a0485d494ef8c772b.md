<!-- YAML
added: v10.10.0
-->

* `pid` {integer} The process ID to retrieve scheduling priority for.
  **Default** `0`.
* Returns: {integer}

The `os.getPriority()` method returns the scheduling priority for the process
specified by `pid`. If `pid` is not provided, or is `0`, the priority of the
current process is returned.

