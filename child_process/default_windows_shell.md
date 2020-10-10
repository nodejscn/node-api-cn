
尽管微软指定在根环境中 `%COMSPEC%` 必须包含 `'cmd.exe'` 的路径，但子进程并不总是遵循相同的要求。
因此，在可以衍生 shell 的 `child_process` 函数中，如果 `process.env.ComSpec` 不可以，则使用 `'cmd.exe'` 作为后备。


