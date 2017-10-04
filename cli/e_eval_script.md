<!-- YAML
added: v0.5.2
changes:
  - version: v5.11.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: Built-in libraries are now available as predefined variables.
-->

把跟随的参数作为 JavaScript 来执行。
在 REPL 中预定义的模块也可以在 `script` 中使用。

*Note*: On Windows, using `cmd.exe` a single quote will not work correctly
because it only recognizes double `"` for quoting. In Powershell or
Git bash, both `'` and `"` are usable.
