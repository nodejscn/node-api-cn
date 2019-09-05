<!-- YAML
added: v2.0.0
-->

* `id` {string|number} 组名或 ID。

`process.setegid()` 方法为进程设置有效的组标识。（参阅 setegid(2)）。
`id` 可以传入数字 ID 或组名字符串。
如果指定了组名，则此方法在解析关联的数字 ID 时会阻塞。

```js
if (process.getegid && process.setegid) {
  console.log(`当前的 gid: ${process.getegid()}`);
  try {
    process.setegid(501);
    console.log(`新的 gid: ${process.getegid()}`);
  } catch (err) {
    console.log(`无法设置 gid: ${err}`);
  }
}
```

这个函数只在 POSIX 平台有效（在 Windows 或 Android 平台无效）。
此特性在 [`Worker`] 线程中不可用。

