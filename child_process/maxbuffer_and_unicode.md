
`maxBuffer` 选项指定了 `stdout` 或 `stderr` 上允许的字节数的最大值。
如果超过这个值，则子进程会被终止。
这会影响包含多字节字符编码的输出，如 UTF-8 或 UTF-16。
例如，`console.log('中文测试')` 会发送 13 个 UTF-8 编码的字节到 `stdout`，尽管只有 4 个字符。

