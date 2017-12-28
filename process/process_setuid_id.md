<!-- YAML
added: v0.1.28
-->

`process.setuid(id)` 设置进程的用户ID (参见
setuid(2).)  `id` 可以是一个数值ID也可以是一个用户名字符串.
如果已经有一个用户名，在解析为相关的数值ID时，此方法阻塞。

```js
if (process.getuid && process.setuid) {
  console.log(`Current uid: ${process.getuid()}`);
  try {
    process.setuid(501);
    console.log(`New uid: ${process.getuid()}`);
  } catch (err) {
    console.log(`Failed to set uid: ${err}`);
  }
}
```

注意: 这个方法只在POSIX平台可用(换句话说，Windows或Android不行)。


