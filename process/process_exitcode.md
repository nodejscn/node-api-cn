<!-- YAML
added: v0.11.8
-->

* {integer}

当进程正常结束，或通过[`process.exit()`][]结束但未传递参数时，此数值标识进程结束的状态码。

给[`process.exit(code)`][`process.exit()`]指定一个状态码，会覆盖`process.exitCode`的原有值。


