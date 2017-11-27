<!-- YAML
added: v2.0.0
-->

* `id` {string|number} A group name or ID

`process.setegid()`方法为进程设置有效的用户组ID。(请看 setegid(2).)
`id`可以传一个数值ID或传一个用户组名称字符串。如果传了后者的话，会解析成一个相关的数值ID，
解析的时候，这个方法方法是阻塞的。

```js
if (process.getegid && process.setegid) {
  console.log(`Current gid: ${process.getegid()}`);
  try {
    process.setegid(501);
    console.log(`New gid: ${process.getegid()}`);
  } catch (err) {
    console.log(`Failed to set gid: ${err}`);
  }
}
```

*注意*: 这个方法只在POSIX平台可用(换句话说，Windows或Android不行)。

