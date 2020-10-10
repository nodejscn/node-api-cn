<!-- YAML
added: v10.10.0
-->

* {Set}

`process.allowedNodeEnvironmentFlags` 属性是 [`NODE_OPTIONS`] 环境变量中允许的特殊只读标志的 `Set`。

`process.allowedNodeEnvironmentFlags` 扩展了 `Set`，但重写了 `Set.prototype.has` 以识别几种不同的可能标志的表示。
在以下情况下，`process.allowedNodeEnvironmentFlags.has()` 将会返回 `true`：

- 标志可以省略前导单（`-`）或双（`--`）破折号。例如，`inspect-brk` 用于 `--inspect-brk`，或 `r` 用于 `-r`。
- 传给 V8 的标志（如 `--v8-options` 中所列）可以替换下划线的一个或多个非前导短划线，反之亦然。例如，`--perf_basic_prof`、`--perf-basic-prof`、`--perf_basic-prof` 等。
- 标志可以包含一个或多个等号（`=`）字符。包含第一个等号后的所有字符都将被忽略。例如，`--stack-trace-limit=100`。
- 在 [`NODE_OPTIONS`] 中必须允许标志。

当迭代 `process.allowedNodeEnvironmentFlags` 时，标志只出现一次。
每个都将会以一个或多个破折号开头。
传给 V8 的标志将包含下划线而不是非前导破折号：

```js
process.allowedNodeEnvironmentFlags.forEach((flag) => {
  // -r
  // --inspect-brk
  // --abort_on_uncaught_exception
  // ...
});
```

`process.allowedNodeEnvironmentFlags` 的 `add()`、`clear()` 和 `delete()` 方法不执行任何操作，并且将会以静默方式失败。

如果在没有 [`NODE_OPTIONS`] 支持的情况下编译 Node.js（在 [`process.config`] 中显示），则 `process.allowedNodeEnvironmentFlags` 将会包含允许的内容。

