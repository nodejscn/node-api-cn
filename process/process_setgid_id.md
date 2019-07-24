<!-- YAML
added: v0.1.31
-->

* `id` {string|number} 进程组名字或ID

`process.setgid()` 为进程方法设置组ID. (查看setgid(2).)
可给`id`参数传一个数值ID或字符串名。

如果已经有一个进程组ID名，那么在解析为相关的ID之前，此方法是阻塞。

```js
if (process.getgid && process.setgid) {
  console.log(`Current gid: ${process.getgid()}`);
  try {
    process.setgid(501);
    console.log(`New gid: ${process.getgid()}`);
  } catch (err) {
    console.log(`Failed to set gid: ${err}`);
  }
}
```

注意: 这个方法只在POSIX平台可用(换句话说，Windows或Android不行)。

