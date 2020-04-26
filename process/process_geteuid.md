<!-- YAML
added: v2.0.0
-->

* 返回: {Object}

`process.geteuid()` 方法返回 Node.js 进程的有效数字标记的用户身份（参见 geteuid(2)）。

```js
if (process.geteuid) {
  console.log(`当前的 uid: ${process.geteuid()}`);
}
```

这个函数只在 POSIX 平台有效（在 Windows 或 Android 平台无效）。

