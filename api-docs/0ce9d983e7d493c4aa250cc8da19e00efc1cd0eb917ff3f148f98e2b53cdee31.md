<!-- YAML
added: v0.1.31
-->

* Returns: {Object}

`process.getgid()`方法返回Node.js进程的数字标记的组身份(See getgid(2))。

```js
if (process.getgid) {
  console.log(`Current gid: ${process.getgid()}`);
}
```

*注意*：这个函数只在POSIX平台有效(在Windows或Android平台无效)。


