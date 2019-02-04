<!-- YAML
added: v0.1.104
-->
* `label` {string} **默认值:** `'default'`。

启动一个计时器，用以计算一个操作的持续时间。
计时器由一个唯一的 `label` 标识。
当调用 [`console.timeEnd()`] 时，可以使用相同的 `label` 来停止计时器，并以毫秒为单位将持续时间输出到 `stdout`。
计时器持续时间精确到亚毫秒。

