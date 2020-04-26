<!-- YAML
added: v2.0.0
-->

`process.getegid()` 方法返回 Node.js 进程的有效数字标记的组身份（参见 getegid(2)）。

```js
if (process.getegid) {
  console.log(`当前的 gid: ${process.getegid()}`);
}
```

这个函数只在 POSIX 平台有效（在 Windows 或 Android 平台无效）。

