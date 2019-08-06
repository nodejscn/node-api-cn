<!-- YAML
added: v0.3.3
-->

* 返回: {string}

`os.release()` 方法返回一个字符串，指定操作系统的发行版。

在 POSIX 系统上，操作系统发行版是通过调用 [uname(3)] 得到的。
在 Windows 系统上, 则使用 `GetVersionExW()`。
详见 https://en.wikipedia.org/wiki/Uname#Examples 。

