<!-- YAML
added: v0.3.3
-->

* Returns: {string}

`os.type()`方法返回一个字符串,表明操作系统的名字,
由uname(3)返回.举个例子, `'Linux'` 在 Linux系统上, `'Darwin'` 在 macOS 系统上,`'Windows_NT'` 在 Windows系统上.

请查看https://en.wikipedia.org/wiki/Uname#Examples 获取其他关于在不同
操作系统上执行uname(3),得到输出的信息.

