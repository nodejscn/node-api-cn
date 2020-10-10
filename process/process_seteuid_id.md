<!-- YAML
added: v2.0.0
-->

* `id` {string|number} 用户名或 ID。

`process.seteuid()` 方法为进程设置有效的用户标识。（参见 seteuid(2)）。
`id` 可以传入数字 ID 或用户名字符串。
如果指定了用户名，则此方法在解析关联的数字 ID 时会阻塞。

```js
if (process.geteuid && process.seteuid) {
  console.log(`当前的 uid: ${process.geteuid()}`);
  try {
    process.seteuid(501);
    console.log(`新的 uid: ${process.geteuid()}`);
  } catch (err) {
    console.log(`无法设置 uid: ${err}`);
  }
}
```

这个函数只在 POSIX 平台有效（在 Windows 或 Android 平台无效）。
此特性在 [`Worker`] 线程中不可用。

