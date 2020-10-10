<!-- YAML
added: v0.5.8
-->

* `eventType` {string} 已发生的更改事件的类型。
* `filename` {string|Buffer} 更改的文件名（如果相关或可用）。

当监视的目录或文件中发生更改时触发。 
在 [`fs.watch()`] 中查看更多详细信息。

可能不提供 `filename` 参数，这取决于操作系统的支持。 
如果提供了 `filename`，则当调用 `fs.watch()` 并将其 `encoding` 选项设置为 `'buffer'` 时，`filename` 将是一个 `Buffer`，否则 `filename` 将是 UTF-8 字符串。

```js
// 使用 fs.watch（）监听器的示例。
fs.watch('./tmp', { encoding: 'buffer' }, (eventType, filename) => {
  if (filename) {
    console.log(filename);
    // 打印: <Buffer ...>
  }
});
```

