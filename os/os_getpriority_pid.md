<!-- YAML
added: v10.10.0
-->

* `pid` {integer} 用于检索调度优先级的进程 ID。**默认值** `0`。
* 返回: {integer}

`os.getPriority()` 方法返回由 `pid` 指定的进程的调度优先级。 
如果未提供 `pid` 或者为 `0`，则返回当前进程的优先级。

