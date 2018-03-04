<!-- YAML
added: v0.9.4
-->

* Returns: {Array}

`process.getgroups()`方法返回数组，其中包含了补充的组ID。
如果包含有效的组ID，POSIX会将其保留为未指定状态，但 Node.js 会确保它始终处于状态。

*注意*：这个函数只在POSIX平台有效(在Windows或Android平台无效)。

