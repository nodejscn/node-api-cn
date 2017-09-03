<!-- YAML
added: v0.5.8
-->

* `eventType` {string} fs 变化的类型
* `filename` {string|Buffer} 变化的文件名（如果是相关的/可用的）

当一个被监视的目录或文件有变化时触发。
详见 [`fs.watch()`]。

`filename` 参数可能不会被提供，这依赖于操作系统支持。
如果提供了 `filename`，则若 `fs.watch()` 被调用时 `encoding` 选项被设置为 `'buffer'` 则它会是一个 `Buffer`，否则 `filename` 是一个字符串。

```js
// 例子，处理 fs.watch 监听器
fs.watch('./tmp', { encoding: 'buffer' }, (eventType, filename) => {
  if (filename) {
    console.log(filename);
    // 输出: <Buffer ...>
  }
});
```

