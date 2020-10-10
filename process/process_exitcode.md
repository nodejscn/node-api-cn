<!-- YAML
added: v0.11.8
-->

* {integer}

当进程正常退出，或通过 [`process.exit()`] 退出且未指定退出码时，此数值将作为进程的退出码。

指定 [`process.exit(code)`][`process.exit()`] 的退出码将覆盖 `process.exitCode` 的原有设置。


