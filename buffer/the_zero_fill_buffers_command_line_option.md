<!-- YAML
added: v5.10.0
-->

可以使用 `--zero-fill-buffers` 命令行选项启动 Node.js，以使所有新分配的 `Buffer` 实例在创建时默认使用零来填充。
如果没有该选项，则使用 [`Buffer.allocUnsafe()`]、[`Buffer.allocUnsafeSlow()`] 和 `new SlowBuffer(size)` 创建的 buffer 不会填充零。
使用这个选项可能会对性能产生重大的负面影响。
仅在需要强制新分配的 `Buffer` 实例不能包含可能敏感的旧数据时，才使用 `--zero-fill-buffers` 选项。

```console
$ node --zero-fill-buffers
> Buffer.allocUnsafe(5);
<Buffer 00 00 00 00 00>
```

