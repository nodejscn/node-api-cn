<!-- YAML
added: v9.0.0
-->

* `path` {string}
* 返回: {string}

仅在 Windows 系统上，返回给定 `path` 的等效[名称空间前缀路径][namespace-prefixed path]。 
如果 `path` 不是字符串，则将返回 `path` 而不进行修改。

此方法仅在 Windows 系统上有意义。 
在 POSIX 系统上，该方法不可操作，并且始终返回 `path` 而不进行修改。


