<!-- YAML
added: v0.1.104
-->
* `label` {string}

启动一个定时器，用以计算一个操作的持续时间。
定时器由一个唯一的 `label` 标识。
当调用 [`console.timeEnd()`] 时，可以使用相同的 `label` 来停止定时器，并以毫秒为单位将持续时间输出到 `stdout`。
定时器持续时间精确到亚毫秒。

