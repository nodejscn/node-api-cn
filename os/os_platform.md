<!-- YAML
added: v0.5.0
-->

* 返回: {string}

返回标识操作系统平台的字符串。
该值在编译时设置。 
可能的值有 `'aix'`、`'darwin'`、`'freebsd'`、`'linux'`、`'openbsd'`、`'sunos'` 和 `'win32'`。

返回的值等价于 [`process.platform`]。

如果 Node.js 在 Android 操作系统上构建，则也可能返回 `'android'` 值。
[Android 的支持是实验性的][Android building]。


