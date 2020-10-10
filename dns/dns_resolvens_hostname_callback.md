<!-- YAML
added: v0.1.90
-->
* `hostname` {string}
* `callback` {Function}
  - `err` {Error}
  - `addresses` {string[]}

使用 DNS 协议为 `hostname` 解析名称服务器记录（`NS` 记录）。
传给 `callback` 函数的 `adresses` 参数将会包含用于 `hostname` 的有效的名称服务器记录的数组（例如 `['ns1.example.com', 'ns2.example.com']`）。

