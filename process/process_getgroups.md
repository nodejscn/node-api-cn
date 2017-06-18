<!-- YAML
added: v0.9.4
-->

* Returns: {Array}

`process.getgroups()`方法返回数组，其中包含了补充的组ID。
POSIX leaves it unspecified if the effective group ID is included but
Node.js ensures it always is.

*注意*：这个函数只在POSIX平台有效(在Windows或Android平台无效)。

