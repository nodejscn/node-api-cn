<!-- YAML
added: v13.11.0
-->

* 返回: {string}

返回一个操作系统内核版本标识的字符串。

在 POSIX 系统中，操作系统版本由调用[`uname(3)`][]决定；在 Windows 系统中, 将会使用 `RtlGetVersion()` ，如果不可用，那么使用 `GetVersionExW()`。在 https://en.wikipedia.org/wiki/Uname#Examples 查看更多信息。

