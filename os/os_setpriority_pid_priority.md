<!-- YAML
added: v10.10.0
-->

* `pid` {integer} 为其设置调度优先级的进程 ID。**默认值** `0`。
* `priority` {integer} 分配给进程的调度优先级。

`os.setPriority()` 方法尝试为 `pid` 指定的进程设置调度优先级。 
如果未提供 `pid` 或者为 `0`，则使用当前进程的优先级。

`priority` 输入必须是 `-20`（高优先级）和 `19`（低优先级）之间的整数。 
由于 Unix 优先级和 Windows 优先级之间的差异，`priority` 会被映射到 `os.constants.priority` 中的六个优先级常量之一。 
当检索进程优先级时，此范围的映射可能导致 Windows 上的返回值略有不同。 
为避免混淆，建议将 `priority` 设置为其中一个优先级常量。

在 Windows 上设置优先级为 `PRIORITY_HIGHEST` 需要提升用户，否则设置优先级将静默地降低到 `PRIORITY_HIGH`。

