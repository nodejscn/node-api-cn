<!-- YAML
added: v6.0.0
-->

* `options` {Object}
  * `encoding` {string} 用于解释结果字符串的字符编码。如果 `encoding` 被设置为 `'buffer'`，则 `username`、`shell` 和 `homedir` 的值将会是 `Buffer` 实例。**默认值:** `'utf8'`。
* 返回: {Object}

`os.userInfo()` 方法返回当前有效用户的信息。
在 POSIX 平台上，这通常是密码文件的子集。
返回的对象包括 `username`、`uid`、`gid`、`shell` 和 `homedir`。
在 Windows 系统上，则 `uid` 和 `gid` 字段是 `-1`，且 `shell` 是 `null`。

`os.userInfo()` 返回的 `homedir` 的值由操作系统提供。
这与 `os.homedir()` 的结果不同，其是在回退到操作系统响应之前查询主目录的几个环境变量。

如果用户没有 `username` 或 `homedir`，则抛出 [`SystemError`]。

