<!-- YAML
added: v0.1.31
-->

* 返回: {Object}

`process.getgid()` 方法返回 Node.js 进程的数字标记的组身份（参见 getgid(2)）。

```js
if (process.getgid) {
  console.log(`当前的 gid: ${process.getgid()}`);
}
```

这个函数只在 POSIX 平台有效（在 Windows 或 Android 平台无效）。


