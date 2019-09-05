<!-- YAML
added: v0.1.28
-->

* 返回: {integer}

`process.getuid()` 方法返回 Node.js 进程的数字标记的用户身份（参阅 getuid(2)）。

```js
if (process.getuid) {
  console.log(`当前的 uid: ${process.getuid()}`);
}
```

这个函数只在 POSIX 平台有效（在 Windows 或 Android 平台无效）。

