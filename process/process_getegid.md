<!-- YAML
added: v2.0.0
-->

`process.getegid()`方法返回Node.js进程的有效数字标记的组身份(See getegid(2))。

```js
if (process.getegid) {
  console.log(`Current gid: ${process.getegid()}`);
}
```

*注意*：这个函数只在POSIX平台有效(在Windows或Android平台无效)。

