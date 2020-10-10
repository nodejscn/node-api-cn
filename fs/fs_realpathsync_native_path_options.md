<!-- YAML
added: v9.2.0
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `encoding` {string} **默认值:** `'utf8'`。
* Returns: {string|Buffer}

同步的 realpath(3)。

仅支持可转换为 UTF8 字符串的路径。

可选的 `options` 参数可以是字符串（指定字符编码）、或具有 `encoding` 属性（指定用于返回的路径的字符编码）的对象。 
如果 `encoding` 被设置为 `'buffer'`，则返回的路径会作为 `Buffer` 对象传入。

在 Linux 上，当 Node.js 与 musl libc 链接时，procfs 文件系统必须挂载在 `/proc` 上才能使此功能正常工作。 
Glibc 没有这个限制。



