<!-- YAML
added: v0.11.10
-->
* `hostname` {string}
* `callback` {Function}
  - `err` {Error}
  - `address` {Object}

使用 DNS 协议为 `hostname` 解析开始权限记录（`SOA` 记录）。
传给 `callback` 函数的 `addresses` 参数将会是一个具有以下属性的对象：

* `nsname`
* `hostmaster`
* `serial`
* `refresh`
* `retry`
* `expire`
* `minttl`

<!-- eslint-skip -->
```js
{
  nsname: 'ns.example.com',
  hostmaster: 'root.example.com',
  serial: 2013101809,
  refresh: 10000,
  retry: 2400,
  expire: 604800,
  minttl: 3600
}
```

