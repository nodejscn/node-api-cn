<!-- YAML
added: v0.1.28
-->

* Returns: {integer}

`process.getuid()`方法返回Node.js进程的数字标记的用户身份(See getuid(2))。

```js
if (process.getuid) {
  console.log(`Current uid: ${process.getuid()}`);
}
```

*注意*：这个函数只在POSIX平台有效(在Windows或Android平台无效)。

