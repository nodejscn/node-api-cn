<!-- YAML
added: v2.0.0
-->

* `id` {string|number} A user name or ID

`process.seteuid()`方法为进程设置有效的用户ID。(请看 seteuid(2).)
`id`可以传一个数值ID或传一个用户名字符串。如果传了特定的用户名字符串，会解析成一个相关的数值ID，
解析的时候，这个方法方法是阻塞的。

```js
if (process.geteuid && process.seteuid) {
  console.log(`Current uid: ${process.geteuid()}`);
  try {
    process.seteuid(501);
    console.log(`New uid: ${process.geteuid()}`);
  } catch (err) {
    console.log(`Failed to set uid: ${err}`);
  }
}
```

*注意*: 这个方法只在POSIX平台可用(换句话说，Windows或Android不行)。

