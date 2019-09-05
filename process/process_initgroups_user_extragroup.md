<!-- YAML
added: v0.9.4
-->

* `user` {string|number} 用户名称或数字标识符。
* `extra_group` {string|number} 组名称或数字标识符。

`process.initgroups()` 方法读取 `/etc/group` 文件，并且初始化组访问列表，该列表包括了用户所在的所有组。
该方法需要 Node.js 进程有 `root` 访问或者有` CAP_SETGID` 能力才能操作。

删除权限时要小心：

```js
console.log(process.getgroups());         // [ 0 ]
process.initgroups('bnoordhuis', 1000);   // 切换用户。
console.log(process.getgroups());         // [ 27, 30, 46, 1000, 0 ]
process.setgid(1000);                     // 删除 root 的 gid。
console.log(process.getgroups());         // [ 27, 30, 46, 1000 ]
```

这个函数只在 POSIX 平台有效（在 Windows 或 Android 平台无效）。
此特性在 [`Worker`] 线程中不可用。

