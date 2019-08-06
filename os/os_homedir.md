<!-- YAML
added: v2.3.0
-->

* 返回: {string}

`os.homedir()` 方法以字符串的形式返回当前用户的主目录。

在 POSIX 上：
如果定义，则将会使用 `$HOME` 环境变量。 
否则，将会使用[有效的 UID][EUID] 来查找用户的主目录。

在 Windows 上：
如果定义，则将会使用 `USERPROFILE` 环境变量。 
否则，将会是当前用户的配置文件目录的路径。


