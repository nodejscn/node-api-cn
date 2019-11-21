<!-- YAML
added: v0.3.3
-->

* 返回: {string}

以字符串的形式返回操作系统。

在 POSIX 系统上，操作系统的发行版是通过调用 [uname(3)] 判断的。
在 Windows 上, 则使用 `GetVersionExW()`。
详见 https://en.wikipedia.org/wiki/Uname#Examples。

