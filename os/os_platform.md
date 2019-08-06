<!-- YAML
added: v0.5.0
-->

* 返回: {string}

`os.platform()` 方法返回一个字符串，指定 Node.js 编译时的操作系统平台。

当前可能的值有：

* `'aix'`
* `'darwin'`
* `'freebsd'`
* `'linux'`
* `'openbsd'`
* `'sunos'`
* `'win32'`

等价于 [`process.platform`]。

如果 Node.js 在 Android 操作系统上构建，则可能返回 `'android'` 值。
但是，Node.js 中的 Android 支持目前被视为是[试验的][Android building]。


