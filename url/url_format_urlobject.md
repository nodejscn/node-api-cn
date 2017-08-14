<!-- YAML
added: v0.1.25
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7234
    description: URLs with a `file:` scheme will now always use the correct
                 number of slashes regardless of `slashes` option. A false-y
                 `slashes` option with no protocol is now also respected at all
                 times.
-->

* `urlObject` {Object|string} 一个 URL 对象（就像 `url.parse()` 返回的）。
  如果是一个字符串，则通过 `url.parse()` 转换为一个对象。

`url.format()` 方法返回一个从 `urlObject` 格式化后的 URL 字符串。

如果 `urlObject` 不是一个对象或字符串，则 `url.parse()` 抛出 [`TypeError`]。

格式化过程如下：

* 创建一个新的空字符串 `result`。
* 如果 `urlObject.protocol` 是一个字符串，则它会被原样添加到 `result`。
* 否则，如果 `urlObject.protocol` 不是 `undefined` 也不是一个字符串，则抛出 [`Error`]。
* 对于不是以 `:` 结束的 `urlObject.protocol`，`:` 会被添加到 `result`。
* 如果以下条件之一为真，则 `//` 会被添加到 `result`：
    * `urlObject.slashes` 属性为真；
    * `urlObject.protocol` 以 `http`、`https`、`ftp`、`gopher` 或 `file` 开头；
* 如果 `urlObject.auth` 属性的值为真，且 `urlObject.host` 或 `urlObject.hostname` 不为 `undefined`，则 `urlObject.auth` 会被添加到 `result`，且后面带上 `@`。
* 如果 `urlObject.host` 属性为 `undefined`，则：
  * 如果 `urlObject.hostname` 是一个字符串，则它会被添加到 `result`。
  * 否则，如果 `urlObject.hostname` 不是 `undefined` 也不是一个字符串，则抛出 [`Error`]。
  * 如果 `urlObject.port` 属性的值为真，且 `urlObject.hostname` 不为 `undefined`：
    * `:` 会被添加到 `result`。
    * `urlObject.port` 的值会被添加到 `result`。
* 否则，如果 `urlObject.host` 属性的值为真，则 `urlObject.host` 的值会被添加到 `result`。
* 如果 `urlObject.pathname` 属性是一个字符串且不是一个空字符串：
  * 如果 `urlObject.pathname` 不是以 `/` 开头，则 `/` 会被添加到 `result`。
  * `urlObject.pathname` 的值会被添加到 `result`。
* 否则，如果 `urlObject.pathname` 不是 `undefined` 也不是一个字符串，则抛出 [`Error`]。
* 如果 `urlObject.search` 属性为 `undefined` 且 `urlObject.query` 属性是一个 `Object`，则 `?` 会被添加到 `result`，后面跟上把 `urlObject.query` 的值传入 [`querystring`] 模块的 `stringify()` 方法的调用结果。
* 否则，如果 `urlObject.search` 是一个字符串：
  * 如果 `urlObject.search` 的值不是以 `?` 开头，则 `?` 会被添加到 `result`。
  * `urlObject.search` 的值会被添加到 `result`。
* 否则，如果 `urlObject.search` 不是 `undefined` 也不是一个字符串，则抛出 [`Error`]。
* 如果 `urlObject.hash` 属性是一个字符串：
  * 如果 `urlObject.hash` 的值不是以 `#` 开头，则 `#` 会被添加到 `result`。
  * `urlObject.hash` 的值会被添加到 `result`。
* 否则，如果 `urlObject.hash` 属性不是 `undefined` 也不是一个字符串，则抛出 [`Error`]。
* 返回 `result`。


