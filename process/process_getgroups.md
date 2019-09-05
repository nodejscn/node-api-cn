<!-- YAML
added: v0.9.4
-->

* 返回: {integer[]}

`process.getgroups()` 方法返回数组，其中包含了补充的组 ID。
如果包含有效的组 ID，则 POSIX 会将其保留为未指定状态，但 Node.js 会确保它始终处于状态。

这个函数只在 POSIX 平台有效（在 Windows 或 Android 平台无效）。

