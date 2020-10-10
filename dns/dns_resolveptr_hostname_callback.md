<!-- YAML
added: v6.0.0
-->
* `hostname` {string}
* `callback` {Function}
  - `err` {Error}
  - `addresses` {string[]}

使用 DNS 协议为 `hostname` 解析指针记录（`PTR` 记录）。
传给 `callback` 函数的 `addresses` 参数将会是一个包含回复记录的字符串数组。

