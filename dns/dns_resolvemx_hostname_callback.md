<!-- YAML
added: v0.1.27
-->
* `hostname` {string}
* `callback` {Function}
  - `err` {Error}
  - `addresses` {Object[]}

使用 DNS 协议为 `hostname` 解析邮件交换记录（`MX` 记录）。
传给 `callback` 函数的 `adresses` 参数将会包含具有 `priority` 和 `exchange` 属性的对象的数组（例如：`[{priority: 10, exchange: 'mx.example.com'}, ...]`）。

