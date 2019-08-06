<!-- YAML
added: v0.3.3
-->

* 返回: {string}

`os.type()` 方法返回一个字符串，表明由 [uname(3)] 返回的操作系统的名字。
例如，在 Linux 系统上是 `'Linux'`，在 macOS 系统上是 `'Darwin'`，在 Windows 系统上是 `'Windows_NT'`。

请查看 https://en.wikipedia.org/wiki/Uname#Examples 获取其他关于在不同操作系统上执行 [uname(3)] 得到输出的信息。

