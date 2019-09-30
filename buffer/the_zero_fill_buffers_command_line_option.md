<!-- YAML
added: v5.10.0
-->

可以使用 `--zero-fill-buffers` 命令行选项启动 Node.js，以使所有新分配的 `Buffer` 实例在创建时默认使用零来填充。
在 Node.js 8.0.0 之前，这包括 `new Buffer(size)`、[`Buffer.allocUnsafe()`]、[`Buffer.allocUnsafeSlow()`] 和 `new SlowBuffer(size)` 分配的 buffer。
从 Node.js 8.0.0 开始，无论是否使用此选项，使用 `new` 分配的 buffer 始终用零填充。
使用这个选项可能会对性能产生重大的负面影响。
建议仅在需要强制新分配的 `Buffer` 实例不能包含可能敏感的旧数据时，才使用 `--zero-fill-buffers` 选项。

```console
$ node --zero-fill-buffers
> Buffer.allocUnsafe(5);
<Buffer 00 00 00 00 00>
```

