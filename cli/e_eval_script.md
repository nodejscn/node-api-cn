<!-- YAML
added: v0.5.2
changes:
  - version: v5.11.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: Built-in libraries are now available as predefined variables.
-->

把跟随的参数作为 JavaScript 来执行。
在 REPL 中预定义的模块也可以在 `script` 中使用。

在 Windows 上，使用 `cmd.exe` 单引号将会无法正常工作，因为它只识别双引号 `"`。
在 Powershell 或 Git bash 中，`'` 和 `"` 都可用。

