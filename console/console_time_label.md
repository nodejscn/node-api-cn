<!-- YAML
added: v0.1.104
-->
* `label` {string} **默认值:** `'default'`。

启动一个计时器，用以计算一个操作的持续时间。
计时器由一个唯一的 `label` 标识。
当调用 [`console.timeEnd()`] 时，可以使用相同的 `label` 来停止计时器，并以合适的时间单位将持续时间输出到 `stdout`。
例如，如果持续时间为 3869 毫秒，则 `console.timeEnd()` 显示 "3.869s"。

