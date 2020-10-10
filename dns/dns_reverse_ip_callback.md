<!-- YAML
added: v0.1.16
-->
* `ip` {string}
* `callback` {Function}
  - `err` {Error}
  - `hostnames` {string[]}

执行一个反向 DNS 查询，将 IPv4 或 IPv6 地址解析为主机名数组。

当出错时，`err` 是一个 [`Error`] 对象，其中 `err.code` 是 [DNS 错误码][DNS error codes]之一。

