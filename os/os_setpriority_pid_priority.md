<!-- YAML
added: v10.10.0
-->

* `pid` {integer} 为其设置调度优先级的进程 ID。**默认值** `0`。
* `priority` {integer} 分配给进程的调度优先级。

尝试为 `pid` 指定的进程设置调度优先级。 
如果未提供 `pid` 或者为 `0`，则使用当前进程的进程 ID。

`priority` 输入必须是 `-20`（高优先级）到 `19`（低优先级）之间的整数。 
由于 Unix 优先级和 Windows 优先级之间的差异，`priority` 会被映射到 `os.constants.priority` 中的六个优先级常量之一。 
当检索进程的优先级时，此范围的映射可能导致 Windows 上的返回值略有不同。 
为避免混淆，应将 `priority` 设置为优先级常量之一。

在 Windows 上，将优先级设置为 `PRIORITY_HIGHEST` 需要较高的用户权限。
否则，设置的优先级将会被静默地降低为 `PRIORITY_HIGH`。

