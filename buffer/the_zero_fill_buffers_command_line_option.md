<!-- YAML
added: v5.10.0
-->

Node.js 可以在一开始就使用 `--zero-fill-buffers` 命令行选项强制所有使用 `new Buffer(size)` 、[`Buffer.allocUnsafe()`] 、[`Buffer.allocUnsafeSlow()`] 或 `new SlowBuffer(size)` 新分配的 `Buffer` 实例在创建时**自动用 0 填充**。
使用这个选项会**改变**这些方法的**默认行为**，且**对性能有明显的影响**。
建议只在需要强制新分配的 `Buffer` 实例不能包含潜在的敏感数据时才使用 `--zero-fill-buffers` 选项。

例子：

```txt
$ node --zero-fill-buffers
> Buffer.allocUnsafe(5);
<Buffer 00 00 00 00 00>
```

