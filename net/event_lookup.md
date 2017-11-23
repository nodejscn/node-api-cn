<!-- YAML
added: v0.11.3
changes:
  - version: v5.10.0
    pr-url: https://github.com/nodejs/node/pull/5598
    description: The `host` parameter is supported now.
-->

在找到主机之后创建连接之前触发。不可用于 UNIX socket。

* `err` {Error|null} 错误对象。查看 [`dns.lookup()`][]。
* `address` {string} IP 地址。
* `family` {string|null} 地址类型。查看 [`dns.lookup()`][]。
* `host` {string} 主机。
