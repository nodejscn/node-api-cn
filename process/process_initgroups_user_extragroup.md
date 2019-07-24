<!-- YAML
added: v0.9.4
-->

* `user` {string|number} 用户名称或数字标识符。
* `extra_group` {string|number} 组名称或数字标识符。

`process.initgroups()`方法读取`/etc/group`文件，并且初始化组访问列表，该列表包括了用户所在的所有组。
该方法需要Node.js进程有`root`访问或者有`CAP_SETGID` capability才能操作。

替换gid并舍弃权限时需要格外谨慎。例如：

```js
console.log(process.getgroups());         // [ 0 ]
process.initgroups('bnoordhuis', 1000);   // switch user
console.log(process.getgroups());         // [ 27, 30, 46, 1000, 0 ]
process.setgid(1000);                     // drop root gid
console.log(process.getgroups());         // [ 27, 30, 46, 1000 ]
```

*注意*：这个函数只在POSIX平台有效(在Windows或Android平台无效)。

