<!-- YAML
added: v0.1.104
-->

* {string}

`process.title` 属性用于获取或设置当前进程在 `ps` 命令中显示的进程名字

*Note*: When a new value is assigned, different platforms will impose
different maximum length restrictions on the title. Usually such restrictions
are quite limited. For instance, on Linux and macOS, `process.title` is limited
to the size of the binary name plus the length of the command line arguments
because setting the `process.title` overwrites the `argv` memory of the
process.  Node.js v0.8 allowed for longer process title strings by also
overwriting the `environ` memory but that was potentially insecure and
confusing in some (rather obscure) cases.

