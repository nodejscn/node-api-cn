<!-- YAML
added: v0.5.0
-->

* Returns: {string}

`os.platform()` 方法返回一个字符串, 指定Node.js编译时的操作系统平台

当前可能的值有:

* `'aix'`
* `'darwin'`
* `'freebsd'`
* `'linux'`
* `'openbsd'`
* `'sunos'`
* `'win32'`

等价于 [`process.platform`][].

*注意*: 如果Node.js 在Android操作系统上构建, `'android'`值
可能被返回. 然而, Android支持Node.js在当前被认为是实验期.

