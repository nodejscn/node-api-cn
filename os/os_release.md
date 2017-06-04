<!-- YAML
added: v0.3.3
-->

* Returns: {string}

`os.release()`方法返回一个字符串, 指定操作系统的发行版.

*注意*: 在POSIX系统上, 操作系统发行版是通过
调用uname(3)得到的. 在 Windows系统上, 用`GetVersionExW()` . 请查看
https://en.wikipedia.org/wiki/Uname#Examples 获取更多信息.

