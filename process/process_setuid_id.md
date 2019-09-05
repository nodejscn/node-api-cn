<!-- YAML
added: v0.1.28
-->
* `id` {integer | string}

`process.setuid(id)` 方法为进程设置用户标识。（参阅 setuid(2)）。
`id` 可以传入数字 ID 或用户名字符串。
如果指定了用户名，则此方法在解析关联的数字 ID 时会阻塞。

```js
if (process.getuid && process.setuid) {
  console.log(`当前的 uid: ${process.getuid()}`);
  try {
    process.setuid(501);
    console.log(`新的 uid: ${process.getuid()}`);
  } catch (err) {
    console.log(`无法设置 uid: ${err}`);
  }
}
```

这个函数只在 POSIX 平台有效（在 Windows 或 Android 平台无效）。
此特性在 [`Worker`] 线程中不可用。

