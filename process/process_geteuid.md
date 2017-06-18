<!-- YAML
added: v2.0.0
-->

* Returns: {Object}

`process.geteuid()`方法返回Node.js进程的有效数字标记的用户身份(See geteuid(2))。

```js
if (process.geteuid) {
  console.log(`Current uid: ${process.geteuid()}`);
}
```

*注意*：这个函数只在POSIX平台有效(在Windows或Android平台无效)。

