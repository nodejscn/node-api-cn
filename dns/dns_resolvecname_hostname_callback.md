<!-- YAML
added: v0.3.2
-->
* `hostname` {string}
* `callback` {Function}
  - `err` {Error}
  - `addresses` {string[]}

使用 DNS 协议为 `hostname` 解析 `CNAME` 记录。
传给 `callback` 函数的 `adresses` 参数将会包含可用于 `hostname` 的规范名称记录的数组（例如：`['bar.example.com']`）。

