<!-- YAML
added: v5.10.0
-->

使用 `--zero-fill-buffers` 命令行选项时，`new Buffer(size)`、[`Buffer.allocUnsafe()`] 、[`Buffer.allocUnsafeSlow()`] 或 `new SlowBuffer(size)` 返回的 `Buffer` 在创建时会用 0 填充。

例子：

```txt
$ node --zero-fill-buffers
> Buffer.allocUnsafe(5);
<Buffer 00 00 00 00 00>
```

