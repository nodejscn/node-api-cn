<!-- YAML
added: v10.12.0
-->

* `path` {string} 要转换为文件 URL 的路径。
* 返回: {URL} 文件 URL 对象。

此函数可确保 `path` 会被解析为绝对路径，并在转换为文件 URL 时正确编码 URL 控制字符。

```js
new URL(__filename);                // 错误: throws (POSIX)
new URL(__filename);                // 错误: C:\... (Windows)
pathToFileURL(__filename);          // 正确:   file:///... (POSIX)
pathToFileURL(__filename);          // 正确:   file:///C:/... (Windows)

new URL('/foo#1', 'file:');         // 错误: file:///foo#1
pathToFileURL('/foo#1');            // 正确:   file:///foo%231 (POSIX)

new URL('/some/path%.c', 'file:'); // 错误: file:///some/path%.c
pathToFileURL('/some/path%.c');    // 正确:   file:///some/path%25.c (POSIX)
```

